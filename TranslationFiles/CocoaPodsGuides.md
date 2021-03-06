#Getting Started with CocoaPods
#CocoaPods指南
--
###CocoaPods安装
以下内容来自[CocoaPods.org](https://guides.cocoapods.org/using/getting-started.html)
#####0. 什么是CocoaPods?

CocoaPods帮助管理你的Xcode项目依赖库。

你的项目依赖库在一个叫Podfile的文本文件中声明。CocoaPods会解决这些库之间的依赖关系，获取生成的源代码，然后将这些库连接到一个Xcode工作空间来创建你的项目。

最终目标是要通过创建一个更集中的生态来提高可发现性，可参与性的第三方开源库。

####1. 现在开始吧！
#####1.1 安装CocoaPods

CocoaPods是用Ruby创建的，所有CocoaPods需要在Ruby环境下才能安装，而Ruby是OS X系统自带的。你可以使用Ruby版本管理器。除非你知道自己在干什么，不然，我们还是建议你在OS X上使用标准Ruby。

在安装gems时，使用默认Ruby安装需要你使用`sudo`命令。(尽管这是在安装gem过程中唯一会出现的问题)。

`$ sudo gem install cocoapods`

如何你在安装过程中，遇到任何问题，请访问[疑难解答](https://github.com/Kito0615/Translations/blob/master/TranslationFiles/CocoaPodsGuides.md#疑难解答).
#####1.2 非超级管理员安装

如果你在这个过程中不想授予RubyGems管理员特权，你可以通过设置`gem install`的`--user-install`标识指向用户路径告诉RubyGems将RubyGems安装到指定的用户目录下，也可以通过设置RubyGems环境变量来实现。后者是我们认为最好的解决办法。如果这样做，需要在用户主目录下创建并修改`.podfile`文件，添加或修改的内容如下:

>`export GEM_HOME=$HOME/.gem`

>`export PATH=$GEM_HOME/bin:/$PATH`

注意，如果你使用了`--user-install`选项，你还需要设置在`.podfile`设置`PATH`参数或在使用这个命令前注入路径。你可以通过`gem which cocoapods`查看gem的安装位置。
使用实例:

>`$ gem install cocoapods --user-install`

>`$ gem which cocoapods`

>`/Users/eloy/.gem/ruby/2.0.0/gems/cocoapods-0.29.0/lib/cocoapods.rb`

>`$ /Users/eloy/.gem/ruby/2.0.0/bin/pod install`

#####1.3 升级CocoaPods

要升级CocoaPods，你只需要重新安装一下gem就可以了。

>`$ [sudo] gem install cocoapods`

或者，安装预览版

>`$ [sudo] gem install cocoapods --pre`

如果你第一次就使用全了超级管理员权限`sudo`安装CocoaPods gem，那么你需要再次使用`sudo`命令来升级。

然后，当你经常使用CocoaPods来安装pods时，当有新版的CocoaPods可以使用时，你会收到诸如_CocoaPods X.X.X is now available, please update_这样的信息提示。

#####1.4 使用CocoaPods命令

有两种方式可以使用CocoaPods命令，一种是使用[Gemfile](https://guides.cocoapods.org/using/a-gemfile.html)(推荐)，一种是在讨论或实际阶段使用[开发版](https://guides.cocoapods.org/using/unreleased-features)。

####其他资源

[CocoaPods at Treehouse](https://teamtreehouse.com/library/ios-tools/cocoapods/cocoapods)
--
###使用CocoaPods
####向Xcode项目中添加Pods

**写在前面**

1. 检查[Specs](https://github.com/CocoaPods/Specs/)仓库或检查网站[cocoapods.org](https://cocoapods.org/)确保你想使用的库是可用的。

2. 在你的电脑上[安装CocoaPods](https://guides.cocoapods.org/using/getting-started.html)

#####安装

* 创建[Podfile](https://guides.cocoapods.org/using/the-podfile.html)，添加你的依赖库:

>`target 'MyApp' do`

>`	pod 'AFNetworking', '~>3.0'`

>`	pod 'FBSDKCoreKit', '~>4.9'`

>`end`

* 在你的工程目录执行`$ pod install`命令。
* 打开`App.xcworkspace`并开始工作。

#####使用CocoaPods创建一个新Xcode项目
要使用CocoaPods创建一个新项目，只需要以下几个简单的步骤:

* 正常使用Xcode创建一个新工程。
* 打开终端窗口，使用`$ cd`命令进入到工程所有目录。
* 创建Podfile. 可以通过`$ pod init`命令完成。
* 打开Podfile.第一行需要指明支持的系统及版本.

>`platform: ios, '9.0'`

* 要使用CocoaPods，你需要定义Xcode目标并连接它们。例如，如果你准备写一个iOS程序，那Xcode目标就是你的app。通过在`target '$TARGET_NAME' do`和`end`之间使用几行代码创建目标
* 通过使用`pod '$PODNAME'`在目标块之间添加一个CocoaPods

>`target 'MyApp' do`

>`	pod 'ObjectiveSugar'`

>`end`

* 保存Podfile
* 执行`$ pod install`命令
* 打开创建的`MyApp.xcworkspace`项目。以后就使用这个文件作为你创建app的每天要使用文件。

#####集成已经存在的工作空间

使用CocoaPods集成已经存在的工作空间需要在Podfile中增加一行。在目标块外面简单声明`.xcworkspace`文件的文件名。

>`workspace 'MyWorkspace'`

####什么时候使用__pod install__,使用时候使用__pod update__?

许多人都比较疑惑，什么时候应该用`pod install`, 什么时候应该用`pod update`。特别是在他们应该使用`pod install`的时候却经常使用`pod update`.

你可以在[pod install vs pod update](https://github.com/Kito0615/Translations/blob/master/TranslationFiles/Getting_Started_With_CocoaPods.md#pod-install-vs-pod-update)这篇这文章中找到关于什么时候该使用哪个命令以及每个命令的目的是什么的更详细的解释。

#####我应该将Pods路径加入到代码控制当中吗？

是否将Pods文件夹添加到代码控制中完全取决于你自己，因为工作流在项目之间不断变化。我们建议你将Pods目录添加到代码管理当中，而不是添加到`.gitignore`文件当中。但是最终的决定权在于你:

#####添加Pods目录到代码管理的好处

* 在复制项目(仓库)之后，立即编译和执行工程，甚至都没有在机器上安装CocoaPods。就没有必要执行`pod install`了，而且不能连接网络。
* 即使Pod源(如:GitHub)失效了，Pod文件(代码/库)常常也是可用的。
* Pod文件可以在复制项目(仓库)之后，保证是和原来安装的是一样的。

#####忽略Pod目录的好处

* 代码管理项目(仓库)会更小，占用更少的空间。
* 只要源(如:GitHub)的所有Pods可用，CocoaPods会能够自动重新创建安装。(严格来说，当没有使用提交Podfile的哈希值时，无法保证执行`pod install`命令将会获取并重新创建特定的文件。尤其是在Podfile中使用zip压缩文件时)
* 否要将Pod目录添加到代码控制中，`Podfile`和`Podfile.lock`都应该在版本控制中。

####什么是`Podfile.lock`？

这个文件是在执行`pod install`命令之后自动生成的，它记录了每个Pod的版本是什么时候安装的。比如:在Podfile中声明以下依赖库

>`pod ‘RestKit`

执行`pod install`将会安装当前版本的RestKit，造成`Podfile.lock`文件被创建，表示安装的具体版本(如:RestKit 0.10.3).由于`Podfile.lock`文件，在这个假定的项目中以后的某个时间，在一台不同的机器上执行`pod install`命令，将会仍然安装RestKit0.10.3，即使有更新的版本可用。CocoaPods将会首先使用`Podfile.lock`中记录的Pod版本，除非依赖库更新或使用了`pod update`(这会使一个更新的`Podfile.lock`文件生成)命令。这样使用CocoaPods可以避免因为依赖库引发的各种令人头痛的问题。

关于这是怎样工作的，有一个来自Google的不错的视频:[CocoaPods and Lockfiles](https://www.youtube.com/watch?v=H-zK1mEwTe0)

####这些事件背后发生了什么？

在Xcode中，直接引用[ruby source](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/user_project_integrator.rb#L61-L65),进行了以下操作:

1.创建或更新了[工作空间](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/user_project_integrator.rb#L82)

2.如果需要，[将你的工程添加到工作空间](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/user_project_integrator.rb#L88-L94)

3.如果需要，[向工作空间中添加CocoaPods静态库](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/target_installer.rb#L40-L61)

4.添加libPods.a到:[目标=>编译选项=>链接库](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer.rb#L385-L393)

5.向你的app工程中添加CocoaPods[Xcode配置文件](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/user_project_integrator/target_integrator.rb#L112)

6.根据CocoaPods的目标配置更改你app的[目标配置](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/generator/xcconfig/aggregate_xcconfig.rb#L46-L73)

7.根据安装绑定到你app的pods[复制源](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/user_project_integrator/target_integrator.rb#L145)即在添加其他编译选项后添加如下内容到`Script build phase`(脚本编译选项):

>* Shell:/bin/sh
>* Script:${SRCROOT}/Pods/PodsResources.sh

注意，如果CocoaPods静态库已经添加到你的项目中，将跳过第三步。这是基于Jonah Williams的利用[静态库](http://blog.carbonfive.com/2011/04/04/using-open-source-static-libraries-in-xcode-4/)

####Pods和子模块

CocoaPods和git子模块是尝试用来解决非常相似的问题的。都致力于简化包含添加第三方代码到你的项目的过程。子模块是连接到项目的特定提交(提交时间)，而CocoaPods是绑定到开发者发布的版本。

#####更改子模块为CocoaPods

在你决定要全部更改到CocoaPods之前，你要确保你目前使用的库都是可用的。记录下你正在使用的库的版本也是一个不错的想法，然后，你就可以设置CocoaPods为同样版本。逐渐地、一步一步地而不一次性完成这项工作也是一个不错的想法。

步骤如下:
	1.如果你还没有安装CocoaPods的话，请先安装CocoaPods
	2.创建[Podfile](https://guides.cocoapods.org/using/the-podfile.html)
	3.[移除子模块引用](http://davidwalsh.name/git-remove-submodule)
	4.向Podfile中添加你移除掉的引用
	5.执行`pod install`
--
###pod install vs. pod update
####简介

许多刚刚开始使用CocoaPods的人认为好像只有在第一次用CocoaPods设置项目的时候使用`pod install`，以后都使用`pod update`.**但实际并不是这样的。**

这篇指南的目的就是向你们解释什么时候使用`pod install`，什么时候使用`pod update`的。

TL;DR:(too long, don't read)简单说来:

>* 在安装新的Pod到你的项目里时使用`pod install`。**即使你已经有了`Podfile`也已经执行过`pod install`了**，当你向一个已经使用过CocoaPods的项目里添加/删除pods时。
>* 只有当你想要**更新pods到更新的版本**时才使用`pod update [PODNAME]`

####详细说明这两个命令

> 注意:CocoaPods中的`install`和`update`并不准确。它的灵感来自于许多其他依赖库管理器如:[bundler](http://bundler.io/), [RubyGems](https://rubygems.org/)或者[composer](https://getcomposer.org/),这些都有相似的命令，这些命令都与这篇指南中的描述功能一样。

#####pod install

这不仅是在第一次向项目中获取pods(第三方库)时使用的命令，而且每次你编辑Podfile，添加/更新/删除pod的时候也要使用它。

* 每次运行/下载/安装新的pods时使用`pod install`命令，它都会将每个已经安装的每个pods的版本写到Podfile.lock文件中。这个文件记录并且锁定每个pod的安装的版本。
* 当你执行`pod install`命令时，它只解析**不在**`Podfile.lock`列表中依赖库。
	* 对于已经在`Podfile.lock`列表中的pods，`pod install`命令只会下载`Podfile.lock`列表中指定的版本而不会检查是否有更新的版本可用。
	* 对于不在`Podfile.lock`列表中的pods，`pod install`命令会搜索`Podfile`中描述的版本(如:`pod 'MyPod', '~>1.2'`)

####pod outdated

当你执行`pod outdate`命令时，CocoaPods将会列出`Podfile.lock`列表中(即当前已经安装的版本)有更新版本可用的pods。也就是说如果你对在上述列表中的pods执行`pod update PODNAME`命令，这些pod将会被更新-同样也会更新在`Podfile`文件中的规则为匹配更新版本,如:`pod 'MyPod', '~>x.y'`

#####pod update

当你执行`pod update PODNAME`命令时，CocoaPods将会查找PODNAME的更新版本，而不会考虑`Podfile.lock`文件里列举的版本。它将会更新pod到最新版本(只要满足你在`Podfile`文件中的版本规则)

如果你不带pod name执行`pod update`命令，CocoaPods将会更新`Podfile`里每个可能的pod为最新版本。

####高级用法

使用`pod update PODNAME`,你将只可以**更新**指定的pod(根据检查是否有新的版本存在而更新pod)。相反，`pod install`不会尝试更新已经安装版本。

当你向`Podfile`里添加pod时，你应该执行`pod install`命令，而不是`pod update`--想要没有更新已经存在的pod的风险而安装新pod也是同样的操作。

当你想要更新指定(或者所有)pod版本的时候，你才会用到`pod update`.

####提交你的Podfile.lock文件

提醒一下，即使**你的原则是不提交`Pods`目录到你的共享仓库**，**你也应该提交并且确认你的Podfile.lock文件**

否则，就可以破坏上面关于`pod install`能锁定你的pod的安装版本的整个逻辑。

####场景实例:

以下有几种场景实例来模拟在项目周期中可能出现多种状况。

#####场景1:*用户1*创建项目

*用户1*创建一个项目并且希望使用pod`A`,`B`,`C`。它们用这些pod创建一个`Podfile`,并且执行`pod install`

这样将会安装`A`,`B`,`C`三个pod，每个的版本都`1.0.0`

`Podfile.lock`文件将会记录`A`,`B`,`C`三个pod的版本都是`1.0.0`

>顺带说一下，因为那是第一次执行`pod install`并且`Pods.xcodeproj`还不存在，这个命令也会创建`Pods.xcodeprj`和`.xcworkspace`文件，但是那只是这个命令的侧面影响，不是它的主要作用。

#####场景2:*用户1*添加新pod

然后，*用户1*想要添加`D`到`Podfile`中。

然后**它们应该执行`pod install`**，这样即使维护`B`的人在上一次执行`pod install`之后发布版本`1.1.0`，这个项目会继续使用`1.0.0`版本，因为用户1只希望添加`D`，而不希望更新`B`。

>这就是为什么有些人会得到错误结果，因为他们使用了`pod update`命令——他们可能在想"我想要用新的pod更新我的项目"？——而不是使用`pod install`，来安装为项目安装新的pod。

#####场景3:*用户2*加入项目

然后，从来没有在这个项目工作的*用户2*加入到这个团队。他复制了这个项目，并执行了`pod install`。

`Podfile.lock`(应该被提交到git仓库)将能保证他能得到和*用户1*一样版本的pod。

即使`C`的`1.2.0`版本也已经可用了，*用户2*也将能得到`C`的`1.0.0`版本。因为那是`Podfile.lock`文件记录的版本。`C`已经被`Podfile.lock`(从名称就可以看出有锁定的意思)文件*锁定*为`1.0.0`版本。

#####场景4:查找新版本

然后，*用户1*希望检查pod是否有可用的新版本。他执行`pod update`命令，将会得到`B`有新版本`1.1.0`发布，`C`有新版本`1.2.0`发布。

*用户1*决定升级`B`，而不升级`C`；所以他将**执行`pod update B`**来升级`B`到`1.1.0`版本(相应地更改`Podfile.lock`)**但是**保持`C`的版本为`1.0.0`(*不会*升级到`1.2.0`)。

####在`Podfile`中，精确的版本不够用？
有时可能会觉得在`Podfile`中指定精确的pod版本，像`pod 'A', '1.0.0'`可能不能每个人都有与的团队里其他人都有相同的版本。

即使仅仅只想添加一个新pod时，他们有时甚至会用`pod update`命令，认为不会有升级其他pod的风险，因为他们已经在`Podfile`里固定了版本。

但是，**那样并不足以保证上述场景中的*用户1*和*用户2*所有pod总是能得到完全一样的版本。**

一个典型的例子，如果`A`依赖于`A2`，在`A.podspec`中有如下声明`dependency 'A2', '~>3.0'`。这样，在你的`Podfile`中使用使用`pod 'A', '1.0.0'`声明的确能强制使*用户1*和*用户2*都使用`A`的`1.0.0`版本。但是:

	* *用户1*可能以`A2`的`3.4`版本结束(因为那是`A2`的当时的最新版本)
	* 然而当*用户2*加入项目后运行`pod install`时，他可能得到`A2`的`3.5`版本(因为`A2`的维护人员同时发布了一个新的版本)

这就是什么只有使用`Podfile.lock`文件以及恰当地使用`pod install`和`pod update`命令可以保证每个成员在自己的电脑上都能使用相同版本的pod

--
###Podfile
####什么是Podfile？

Podfile是描述一个或多个Xcode项目目标依赖关系的规范。这个文件应该简单命名为`Podfile`。本文以下所有的示例都是按照在CocoaPods1.0及以后版本的规范来写的。

 一个Podfile可以非常简单，下面只是为目标添加了`AFNetworking`。


> target 'MyApp' do

> 	pod 'AFNetworking', '~> 3.0'

> end

 下面是一个稍微复杂的示例，它链接了app到它的测试绑定。

> source 'https://github.com/CocoaPods/Specs.git'

> source 'https://github.com/Artsy/Specs.git'

> 

> platform :ios, '9.0'

> inhibit_all_warnings!

> 

> target 'MyApp' do

> 	pod 'GoogleAnalytics', '~> 3.1'

> 

> 	//Has its own copy of OCMock

>  	//and has access to GoogleAnalytics via the app

> 	//taht hosts the test target

> 

> 	target 'MyAppTests' do

> 		inherit! :search_paths

> 		pod 'OCMock', '~> 2.0.1'

> 	end

> end

> 

> post_install do |installer|

> 	installer.pods_project.targets.each do |target|

> 		puts target.name

> 	end

> end


 如果你想多个目标共享同一个pod，使用`abstract_target`


>//There are no targets called "Show" in any Xcode projects

>//这儿并没有任何一个Xcode项目叫"Show"

> abstract_target 'Shows' do

> 	pod 'ShowsKit'

> 	pod 'Fabric'

>//Has its own copy of ShowsKit + ShowWebAuth

>//拥有它自己的ShowKit和ShowWebAuth的副本

> 	target 'ShowsiOS' do

> 		pod 'ShowWebAuth'

> 	end

>//Has its own copy of ShowsKit + ShowTVAuth

> 	target 'ShowsTV' do

> 		pod 'ShowTVAuth'

> 	end

> end


在Podfile的根目录里隐含了一个绝对目标，因此你也可以将上面示例写成这样:

> pod 'ShowsKit'

> pod 'Fabric'

> 

> //Has its own copy of ShowsKit + ShowWebAuth

> target 'ShowsiOS' do

> 	pod 'ShowWebAuth'

> end

> 

>//Has its own copy of ShowsKit + ShowTVAuth

> target 'ShowsTV' do

> 	pod 'ShowTVAuth'

> end


######从0.x迁移到1.0

我们在[博客](http://blog.cocoapods.org/CocoaPods-1.0/)里深度解释了所作的改变。

######指定pod版本

 当我们开始一个新项目时，你可能希望使用最新版本的Pod。如果是这样，只需要忽略掉版本要求。


> pod 'SSZipArchive'


 以后你可能希望使用指定版本的Pod，这样的话，你可以指定版本编号.


> pod 'Objection', '0.9'

除此之外，没有版本号或不确定版本号，以下逻辑运算也是可以的:

* `> 0.1` 大于版本号为0.1的任何版本
* `>= 0.1` 大于或等于版本号为0.1的任何版本
* `< 0.1` 小于版本号为0.1的任何版本
* `<= 0.1` 小于或等于版本号为0.1的任何版本

CocoaPods除了逻辑运行符之外还有一个开放式运算符(Optimistic Operator)`~>`:

* `~> 0.1.2` 版本号为0.1.2到0.2，不包含0.2及以上版本
* `~> 0.1` 版本号为0.1到1.0，不包含1.0及以上版本
* `~> 0`版本号为0及以上版本，相当于什么也没有写

想要获得更多关于版本规范的信息，请参考:

* [语义版本控制](http://semver.org/)
* [RubyGems版本规范](http://guides.rubygems.org/patterns/#semantic-versioning)
* 这里有一个来自Google的[视频](https://www.youtube.com/watch?v=x4ARXyovvPc)描述了这是怎样工作的。

####使用本地机器中的文件夹中的文件

  如果你想创建一个Pod和它的客户端串联起来，你可以使用`:path`。


> `pod 'AFNetworking`, :path => '~/Documents/AFNetworking'

使用CocoaPods的这个选项会假设给定的路径是Pod的根目录，将会在Pod项目中直接链接这些文件。这意味着你的编辑将会保留在CocoaPods的安装中。引用的目录可以被你收藏的SCM或当前仓库的git子模块检查。

注意:Pod文件的`Podspec`应该在指定的目录中。

######库目录(仓库根目录)中的Podspec文件
有时你可能希望使用Pod的最新版本、特定版本或者你自己创建版本。如果是这样，你可以在Pod声明中指定。

 要使用仓库的`master`分支:

> `pod 'AFNetworking', :git => 'https://github.com/gowalla/AFNetworking.git'`

 要使用仓库的不同分支:

> `pod 'AFNetworking', :git => 'https://github.com/gowalla/AFNetworking.git', :branch => 'dev'`

 要使用仓库的标签:

> `pod 'AFNetworking', :git => 'https://github.com/gowalla/AFNetworking.git', :tag => '0.7.0'`

 要使用特定的提交版本:

> `pod 'AFNetworking', :git => 'https://github.com/gowalla/AFNetworking.git', :commit => '082f8319af'`

值得注意的是，这个方法意味着版本号必须满足其他依赖于这个pod的其他pod。

`podspec`文件应该在仓库的根目录下，如果一个库没有`podspec`文件，你肯定会用到下一节列举的方法之一。

####参考资料

* [Podfile，非凡的艺术性/Eigen](https://github.com/artsy/eigen/blob/master/Podfile)
* [Swfit项目中Podfile的艺术/Eidolon](https://github.com/artsy/eidolon/blob/master/Podfile)

--
###疑难解答
#####安装CocoaPods
* 如果你的电脑是OS X10.9.0～10.9.2，当RubyGems尝试安装`json` gem的时候你可能会遇到问题。请按照这篇[指南](https://gist.github.com/alloy/62326fcbc5b8ef987c17)解决
* 从OS X10.8升级到10.9之后怎么也不能安装CocoaPods，即使重新安装gem也不行。要解决这个问题，你可以需要先卸载再重新安装gem。

> $ gem uninstall cocoapods
> $ gem install cocoapods

* 安装的gem可能不能自动编译，要解决，你可能需要[连接GCC](http://www.relaxdiego.com/2012/02/using-gcc-when-xcode-43-is-installed.html)
* 如果你使用的是预览版Xcode，你可以需要升级command line tools(命令行工具)
* CocoaPods可能与MacRuby不兼容。

#####使用CocoaPods项目

1. 如果有时CocoaPods不正常工作了，首先确保你完全没有修改过项目里的`Pods.xcconfig`的任何编译设置选项。要往你项目里添加项目编译选项，在列表值前面添加`$(inherited)`。
2. 如果Xcode不能找到依赖库的头文件:
	* 检查`Pods/Headers`里的符号连接是否正确，并且你没有修改过`HEADER_SEARCH_PATH`(参考第一条)
	* 确保你的项目正在使用`Pods.xcconfig`文件。要检查这一项，选中你的项目文件，在第二个面板中再选中，然后打开第三个面板中的`Info`标签。在配置选项下面，你应该在每项你安装的pods的配置要求的地方选择`Pods.xcconfig`。
	* 如果你的Xcode仍然找不到它们，最后一个方法你可以在你的imports(导入)前，写上如以下命令:`#import "Pods/SSZipArchive.h"`
3. 如果你得到关于无法识别C编译器的命令行错误，如:

> `cc1obj: error: unrecognised command line options "-Wno-sign-conversion`:

	* 首先保证你的项目[设置](https://img.skitch.com/20111120-brfn4mp8qwrju8w8325wphan9h.png)使用的是"Apple LLVM compiler"(clang)
	* 检查在你的像`~/.profile`文件中是否设置过`CC`、`CPP`、`CXX`这样的环境变量。这可能干预Xcode编译过程。如果有，从`~/.profile`文件中删除掉环境变量。

4. 当Xcode在链接的时候出现如:`Library not found for -lPods`错误时，它并没有检测到隐藏的依赖:
	* 打开`Product`->`Edit Scheme`
	* 选项`Build`标签
	* 添加`Pods`静态库，并保证它在列表的最上方
	* 清除并重新编译
	* 如果上述操作没用，检查你要包含的spec已经从GitHub上获取了。查看目录`<项目路径>/Pods/<你要包含的spec>`。如果里面是空的(它不应该是空的)，检查`~/.cocoapods/master/<spec>/<spec>.cocoapods`里包含的GitHub上路径是正确的。
	* 如果还是不行，检查你的Xcode本地设置。打开`Preferences`->`Locations`->`Derived Data`->`Advanced`,设置编译位置为"Relative to Workspace"
* 如果你准备提交到App Store，打开`Product`->`Archive`发现"Orgnaizer"页面什么也没有:
	* 在Xcode的"Build Settings"选项中，找到"Skip Install"。设置应用程序目标的"Release"为"NO"。再次编译应该可以了。

*不同版本的Xcode可能有不同的问题。向我们救助并告诉我们你使用的版本*

#####在使用静态库时出现"Duplicate Symbol"错误怎么办？
这个错误通常出现在你的程序中使用了包含常用依赖的第三方闭源库的情况。一种方法是从静态库中强制移除这个依赖关系。具体方法请参考[这里](http://atnan.com/blog/2012/01/12/avoiding-duplicate-symbol-errors-during-linking-by-removing-classes-from-static-libraries)

然而，通常情况下，三方库包含的依赖库都有前缀，你不需要去处理它。如果出现了，请联系开发者，让他们修改，然后使用上述方法作为临时操作。

#####在执行pod命令时遇到权限错误
到CocoaPods0.32.0版本的时候，我们移除了pod命令使用root权限来防止当用户混合使用root权限执行CocoaPods进入(权限)相矛盾的状态。

如果你在某一阶段使用root权限执行CocoaPods命令，当你执行到某一操作时，你可能就会遇到权限错误。当你遇到权限错误时，你可能需要删除那些缓存数据中使用root权限旧文件。你可以这样做:

> $ sudo rm -fr ~/Library/Caches/CocoaPods/
> $ sudo rm -fr ~/.cocoapods/repos/master/

同时，那些全局文件，也可能是一个`Pods`目录可能出现在任何包含Podfile的目录。如果你仍然收到权限错误，你应该也要删除那些文件，然后再执行`pod install`.

> $ sudo rm -fr Pods/

#####我想使用master/branch(分支)，但是我被堵塞了。

这里有一篇文章[使用CocoaPods某个版本尝试新功能](https://guides.cocoapods.org/using/unreleased-features)

#####没有找到解决方案

我们有多种支持途径，按我们喜欢的顺序列出:

* [Stack Overflow](http://stackoverflow.com/search?q=CocoaPods), 连接网络。这可以让CocoaPods的开发团队没有压力，并且给我们时间去解决没有解决的问题。
* [CocoaPods团队邮箱列表](http://groups.google.com/group/cocoapods)，这个邮箱列表主要用来发布相关项目和支持。
* 如果你的问题是关于通过CocoaPods发布的库，请参考[spec repo](https://github.com/CocoaPods/Specs)

#####我认为CocoaPods有bug
这种情况我们希望你可以在GitHub的问题追踪版块提出，这样我们用来可以记录我们开发工作。

* __在你新建之前先搜索一下__。如果你有新的总是，请添加到已有项目。
* 
* __只允许关于CocoaPods工具的问题__。包含[CocoaPods](https://github.com/CocoaPods/CocoaPods/issues)、[CocoaPods/Core](https://github.com/CocoaPods/Core/issues)和[Xcodeproj](https://github.com/CocoaPods/Xcodeproj/issues)
* __保证名称简单但好记__。确保你包含的内容可以被用来解决问题。别重复做。好的意见允许我们关注解决问题而不讨论问题。

###常见问题
#####既然Swift有一个内置的包管理器了，CocoaPods会停止开发吗？
正如[Swift包管理器\(SPM\)](https://github.com/apple/swift-package-manager)在[README.md](https://github.com/apple/swift-package-manager/blob/master/README.md)中写道:SPM现在还在开发设计的初期。它现在并不支持iOS, OS X, watch OS或Objective-C。即使SPM在开发，CocoaPods将会继续支持Swift和Objective-C。等到SPM接近成熟的时候，我们将会评估CocoaPods和CocoaPods社区最好的前景。

#####为什么不直接使用Git子模块？
CocoaPods**不是**用来下载代码的。虽然它可以下载，但事实证明那是最不有趣的部分。

CocoaPods的定义是成为依赖库解决方案，就是版本管理和自动集成到Xocde中。

最后，如果你只是找一个下载器，考虑别的吧。事实上，其它一些源代码控制管理(SCM)就是用来下载的。另外，CocoaPods，很多人不知道可以用来处理本地或网络上的Subversion, Mercurial(译者注：前两面两个都SCM)和zip/tarball包。

#####CocoaPods还没有准备好迎接它的黄金时代吗？
正确。1.0.0版本将会成为我们自信满足Cocoa依赖库管理的基本要求的里程碑。

一旦我们达到1.0.0的里程碑，我们将——真正的第一次——通过邮件列表如cocoa-dev联系整个社区。

#####我要怎样给CocoaPods捐赠？
TL;DR:我们非常感激这种想法。但是这个项目(作为一个实体)不接受任何商业捐赠。我们写过一篇[博客](https://blog.cocoapods.org/Why-we-dont-accept-donations/)进行说明。

#####CocoaPods并不能做任何事，所以它没用。
首先，请看第二点。然后，除非你告诉我们缺失的功能并且告诉我们为什么它很重要，否则它不会没用。我们不会费功夫去看Twiter，所以请git上[Issue](https://github.com/CocoaPods/CocoaPods/issues/new)我们，更好的方法是pull-request。

#####CocoaPods并没有做依赖解决方案？
CocoaPods一直都成为依赖解决方案，但是直到0.35版本，才自动上锁冲突解决方案。到现在，CocoaPods已经可以解决任何可以被解决的冲突。

#####CocoaPods在社区功能上欠缺，因为用户使用它很容易就能添加许多依赖库。
这就好比说，"我们不需要汽车，因为它们让我们变懒，让我们忘掉走路/跑步",或者"我们不应该使用集成开发工具([IDEs](http://programmers.stackexchange.com/questions/39798/being-ide-dependent-how-can-it-harm-me/39809#39809))，因为它们让我们成为差劲的程序员，我们不能用文本编辑器写代码，不能记住语法"。另外，这个问题同样适用于任何获取代码的基本的方法(如:git)，所以这个问题不值得讨论。

然而，值得讨论的是告知用户的责任。够讽刺的是，CocoaPods的原作者被“使用太多依赖库是不好的”想法给说服了。想要了解如何解决这个问题更多实用的建议，你应该阅读[Manfred Stienstra](https://twitter.com/manfreds)的这篇[博客](http://www.fngtps.com/2013/a-quick-note-on-minimal-dependencies-in-ruby-on-rails/)

#####CocoaPods使用工作空间，被看作是用户数据。为什么不直接使用常规的子工程？
从Xcode4开始，[苹果为这些目的引入了工作空间](http://developer.apple.com/library/ios/#featuredarticles/XcodeConcepts/Concept-Workspace.html)

自此以后，苹果公司也为每个xcodeproj文档添加了工作空间文件，引导人们相信工作空间只是用户数据。这是不正确的，并且，如果我们这样做了，你**不应该**再忽略工作文件。

需要注意的是，CocoaPods本身并不需要使用工作空间。如果你更喜欢子项目，你可以在命令行执行下面命令:`pod install --no-integrate`，这样就可以按你希望的配置集成到你的项目中。

#####为什么要使用CocoaPods一定要安装Ruby？
你不需要！OS X已经预安装了Ruby2.0.0或更新版本,在`/usr/bin/ruby`目录中，我们是基于这个实现的。
