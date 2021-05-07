# Arthas

Arthas is a Java diagnostic tool。



常用命令：

dashboard                                                                          

trace  com.xxx.poxy getZone '#cost>700 && params[0].equals("intl_pointsmall_tasks")'

 watch  com.xxx.poxy getZon "{params,returnObj}" -x 2