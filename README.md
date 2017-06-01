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
                   
                   
                   
