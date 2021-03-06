#使用命令行操作#

我们可以用Gradle命令来执行特定的任务，运行一个任务需要你知道该任务的名称，如果Gradle能够告诉你有哪些任务可以执行那岂不是很棒？Gradle提供了一个辅助的任务tasks来检查你的构建脚本，然后显示所有的任务，包含一个描述性的消息。

	$ gradle -q tasks
输出如下：
	 
	All tasks runnable from root project
	 
	Build Setup tasks
	 
	setupBuild - Initializes a new Gradle build. [incubating]
	wrapper - Generates Gradle wrapper files. [incubating]
	 
	 
	Help tasks
	----------
	dependencies - Displays the dependencies of root project'grouptherapy'.
	dependencyInsight - Displays the insight into a specific dependency in root
	➥ project 'grouptherapy'.
	help - Displays a help message
	projects - Displays the sub-projects of root project 'grouptherapy'.
	properties - Displays the properties of root project 'grouptherapy'.
	tasks - Displays the tasks runnable from root project 'grouptherapy' (some of
	➥ the displayed tasks may belong to subprojects).

	Other tasks
	-----------
	groupTherapy

	To see all tasks and more detail, run with --all.

Gradle提供任务组的概念，简而言之就是将一些任务归为一组，你可以执行这个组里面所有的任务，没有分组的任务在Other tasks，任务分组后面会讲到。

#任务执行#

要执行一个任务，只需要输入gradle + 任务名，Gradle确保这个任务和它所依赖的任务都会执行，要执行多个任务只需要在后面添加多个任务名。

##任务名称缩写##

Gradle提高效率的一个办法就是能够在命令行输入任务名的驼峰简写，当你的任务名称非常长的时候这很有用，当然你要确保你的简写只匹配到一个任务，比如下面的情况：

	task groupTherapy << {
	...
	}
	task generateTests << {
	...
	}
这时候你使用gradle gT的时候Gradle就会报错，因为有多个任务匹配到gT:  

	$ gradle gT
	FAILURE: Could not determine which tasks to execute.
	* What went wrong:
	Task 'gT' is ambiguous in root project 'grouptherapy'. Candidates are:
	➥ 'generateTests', 'groupTherapy'.
	* Try:
	Run gradle tasks to get a list of available tasks.

	BUILD FAILED

##运行的时候排除一个任务##

比如运行的时候你要排除yayGradle0,你可以使用-x命令来完成

	$ gradle groupTherapy -x yayGradle0
	:yayGradle1
	Gradle rocks
	:yayGradle2
	Gradle rocks
	:groupTherapy
运行的时候Gradle排除了yayGradle0任务和它依赖的任务startSession。

#命令行选项#

* -i:Gradle默认不会输出很多信息，你可以使用-i选项改变日志级别为INFO
* -s:如果运行时错误发生打印堆栈信息
* -q:只打印错误信息
* -?-h,--help:打印所有的命令行选项
* -b,--build-file:Gradle默认执行build.gradle脚本，如果想执行其他脚本可以使用这个命令，比如gradle -b test.gradle
* --offline:在离线模式运行build,Gradle只检查本地缓存中的依赖
* -D, --system-prop:Gradle作为JVM进程运行，你可以提供一个系统属性比如：-Dmyprop=myValue
* -P,--project-prop:项目属性可以作为你构建脚本的一个变量，你可以传递一个属性值给build脚本，比如：-Pmyprop=myValue

-----------------
* tasks:显示项目中所有可运行的任务
* properties:打印你项目中所有的属性值


