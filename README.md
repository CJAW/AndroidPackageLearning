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
                   
                   
                   
