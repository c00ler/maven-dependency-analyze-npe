# Reproducer for the NPE in Maven 4.0.0-alpha4

Run the `dependency:analyze` goal:

```shell
./mvnw dependency:analyze
```

Output should contain a warning message about the `NullPointerExteption`:

```shell
[INFO] <<< dependency:3.5.0:analyze (default-cli) < test-compile @ maven-dependency-analyze-npe <<<
[INFO]
[WARNING] Failed to notify spy org.apache.maven.ReactorReader$ReactorReaderSpy: null
[INFO]
[INFO] --- dependency:3.5.0:analyze (default-cli) @ maven-dependency-analyze-npe ---
```

Stacktrace:

```shell
[WARNING] Failed to notify spy org.apache.maven.ReactorReader$ReactorReaderSpy: null
java.lang.NullPointerException
    at java.util.ArrayDeque.addLast (ArrayDeque.java:304)
    at org.apache.maven.ReactorReader.processEvent (ReactorReader.java:323)
    at org.apache.maven.ReactorReader.access$000 (ReactorReader.java:67)
    at org.apache.maven.ReactorReader$ReactorReaderSpy.onEvent (ReactorReader.java:501)
    at org.apache.maven.eventspy.internal.EventSpyDispatcher.onEvent (EventSpyDispatcher.java:84)
    at org.apache.maven.eventspy.internal.EventSpyExecutionListener.mojoStarted (EventSpyExecutionListener.java:108)
    at org.apache.maven.lifecycle.internal.DefaultExecutionEventCatapult.fire (DefaultExecutionEventCatapult.java:80)
    at org.apache.maven.lifecycle.internal.DefaultExecutionEventCatapult.fire (DefaultExecutionEventCatapult.java:41)
    at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute2 (MojoExecutor.java:333)
    at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute (MojoExecutor.java:324)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:212)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:174)
    at org.apache.maven.lifecycle.internal.MojoExecutor.access$000 (MojoExecutor.java:77)
    at org.apache.maven.lifecycle.internal.MojoExecutor$1.run (MojoExecutor.java:162)
    at org.apache.maven.plugin.DefaultMojosExecutionStrategy.execute (DefaultMojosExecutionStrategy.java:39)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:159)
    at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject (LifecycleModuleBuilder.java:114)
    at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject (LifecycleModuleBuilder.java:80)
    at org.apache.maven.lifecycle.internal.builder.singlethreaded.SingleThreadedBuilder.build (SingleThreadedBuilder.java:60)
    at org.apache.maven.lifecycle.internal.LifecycleStarter.execute (LifecycleStarter.java:132)
    at org.apache.maven.DefaultMaven.doExecute (DefaultMaven.java:313)
    at org.apache.maven.DefaultMaven.doExecute (DefaultMaven.java:228)
    at org.apache.maven.DefaultMaven.execute (DefaultMaven.java:153)
    at org.apache.maven.cli.MavenCli.execute (MavenCli.java:859)
    at org.apache.maven.cli.MavenCli.doMain (MavenCli.java:282)
    at org.apache.maven.cli.MavenCli.main (MavenCli.java:198)
    at jdk.internal.reflect.NativeMethodAccessorImpl.invoke0 (Native Method)
    at jdk.internal.reflect.NativeMethodAccessorImpl.invoke (NativeMethodAccessorImpl.java:62)
    at jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke (DelegatingMethodAccessorImpl.java:43)
    at java.lang.reflect.Method.invoke (Method.java:566)
    at org.codehaus.plexus.classworlds.launcher.Launcher.launchEnhanced (Launcher.java:282)
    at org.codehaus.plexus.classworlds.launcher.Launcher.launch (Launcher.java:225)
    at org.codehaus.plexus.classworlds.launcher.Launcher.mainWithExitCode (Launcher.java:406)
    at org.codehaus.plexus.classworlds.launcher.Launcher.main (Launcher.java:347)
    at jdk.internal.reflect.NativeMethodAccessorImpl.invoke0 (Native Method)
    at jdk.internal.reflect.NativeMethodAccessorImpl.invoke (NativeMethodAccessorImpl.java:62)
    at jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke (DelegatingMethodAccessorImpl.java:43)
    at java.lang.reflect.Method.invoke (Method.java:566)
    at org.apache.maven.wrapper.BootstrapMainStarter.start (BootstrapMainStarter.java:53)
    at org.apache.maven.wrapper.WrapperExecutor.execute (WrapperExecutor.java:152)
    at org.apache.maven.wrapper.MavenWrapperMain.main (MavenWrapperMain.java:76)
[INFO]
```
