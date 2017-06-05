# AndroidPackageLearning
android学习的总结：


                                                  Intent:
                                                  
(1)显示Intent,直接使用intent(Context,class),startActivite或startActiviteForResult()启动。



(2)隐式intent，用于启动不同的应用。请对 Intent 对象调用 resolveActivity()。如果结果为非空，则至少有一个应用能够处理该 Intent，并且可以安全调用 startActivity()。 如果结果为空，则您不应使用该 Intent。如有可能，您应停用调用该 Intent 的功能。
还需要在mainfirst文件中进行配置

intent总结：如果用intent启动服务service应该使用显示的启动。




                                               
                                                      activity
                                                     
                                                     
                                               
                                               
(1)activity 的启动顺序


(2)activity的生命周期


(3)activity的栈


(4）Fragment与activity




                                                       service
                                                 
                                                 
                                                 
如果组件通过调用 startService() 启动服务（这会导致对 onStartCommand() 的调用），则服务将一直运行，直到服务使用 stopSelf() 自行停止运行，或由其他组件通过调用 stopService() 停止它为止。

如果组件是通过调用 bindService() 来创建服务（且未调用 onStartCommand()，则服务只会在该组件与其绑定时运行。一旦该服务与所有客户端之间的绑定全部取消，系统便会销毁它。 


创建绑定服务
绑定服务允许应用组件通过调用 bindService() 与其绑定，以便创建长期连接（通常不允许组件通过调用 startService() 来启动它）。

如需与 Activity 和其他应用组件中的服务进行交互，或者需要通过进程间通信 (IPC) 向其他应用公开某些应用功能，则应创建绑定服务。

要创建绑定服务，必须实现 onBind() 回调方法以返回 IBinder，用于定义与服务通信的接口。然后，其他应用组件可以调用 bindService() 来检索该接口，并开始对服务调用方法。服务只用于与其绑定的应用组件，因此如果没有组件绑定到服务，则系统会销毁服务（您不必按通过 onStartCommand() 启动的服务那样来停止绑定服务）。

要创建绑定服务，首先必须定义指定客户端如何与服务通信的接口。 服务与客户端之间的这个接口必须是 IBinder 的实现，并且服务必须从 onBind() 回调方法返回它。一旦客户端收到 IBinder，即可开始通过该接口与服务进行交互。

多个客户端可以同时绑定到服务。客户端完成与服务的交互后，会调用 unbindService() 取消绑定。一旦没有客户端绑定到该服务，系统就会销毁它。





                                              客户端进行了主件的绑定，需要实现：
                                              
                                              
实现 ServiceConnection。


您的实现必须重写两个回调方法：onServiceConnected()


系统会调用该方法以传递服务的　onBind() 方法返回的 IBinder。（即 onserviceconnected（）方法中的ibinder参数可以调用service的方法，且包涵数据）


onServiceDisconnected()


Android 系统会在与服务的连接意外中断时（例如当服务崩溃或被终止时）调用该方法。当客户端取消绑定时，系统“不会”调用该方法。


调用 bindService()，传递 ServiceConnection 实现。


当系统调用您的 onServiceConnected() 回调方法时，您可以使用接口定义的方法开始调用服务


要断开与服务的连接，请调用 unbindService()。


如果应用在客户端仍绑定到服务时销毁客户端，则销毁会导致客户端取消绑定。 更好的做法是在客户端与服务交互完成后立即取消绑定客户端。 这样可以关闭空闲服务。如需了解有关绑定和取消绑定的适当时机的详细信息，请参阅附加说明。


例如，以下代码段通过扩展 Binder 类将客户端与上面创建的服务相连，因此它只需将返回的 IBinder 转换为 LocalService 类并请求 LocalService 实例：


LocalService mService;

private ServiceConnection mConnection = new ServiceConnection() {


    // Called when the connection with the service is established
    
    
    public void onServiceConnected(ComponentName className, IBinder service) {
    
    
        // Because we have bound to an explicit
        
        
        // service that is running in our own process, we can
        
        
        // cast its IBinder to a concrete class and directly access it.
        
        
        LocalBinder binder = (LocalBinder) service;
        
        
        mService = binder.getService();
        
        
        mBound = true;
    }

    // Called when the connection with the service disconnects unexpectedly
    
    
    public void onServiceDisconnected(ComponentName className) {
    
    
        Log.e(TAG, "onServiceDisconnected");
        
        
        mBound = false;
        
        
    }
    
    
};
 
                   
