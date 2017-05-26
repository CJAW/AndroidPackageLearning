# AndroidPackageLearning
android学习的总结：


                                                  Intent:
                                                  
(1)显示Intent,直接使用intent(Context,class),startActivite或startActiviteForResult()启动。



(2)隐式intent，用于启动不同的应用。请对 Intent 对象调用 resolveActivity()。如果结果为非空，则至少有一个应用能够处理该 Intent，并且可以安全调用 startActivity()。 如果结果为空，则您不应使用该 Intent。如有可能，您应停用调用该 Intent 的功能。
还需要在mainfirst文件中进行配置

intent总结：如果用intent启动服务service应该使用显示的启动。
