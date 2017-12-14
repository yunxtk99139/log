# log

遇到的坑：

company中多人开发，一般是一个帐号是team agent ,其他的team admin ,team member。当需要多人开发打包，一种方式是agent 来使用自己的帐号来生成certificates ,生产对应的app store ,adhoc ,development 的provisioning profile。其他角色帐号（admin,member）下载从agent生成的的钥匙串中私钥的p12文件，安装后可以使用device member中的provisioning profile来开发，打包上传（当时用xcode打包可能有warring,不小心点到renew,revoke后会重新以本机的钥匙串去生成）。第二种方式是没个人自己去生成certificates，provisioning profile。这种方式问题就太多了，每次打包，都需要去把自己生成的provisioning profile设置与自己的证书对应，并且Distrubt证书最多只能生成3个。

个人开发的时候，很多时候不是使用的同一台电脑开发，这样也会遇到上面的两种情况。

 同一的管理证书可以解决很多开发中的证书问题。而使用使用如xcode打包上传，很多步骤需要交互，很浪费时间。

所以使用集成打包可以很好的解决上面的问题。让开发者有更多的精力投入业务开发。

现在的集成大包方案很多。这里只用到了jenkins + fastlane + git +  firim的方案。

开发证书统一使用git存放，fastlane match可以很好的管理证书。

通过fastlane的firim插件上传包到firim

用jenkins保存一组如shell命令的打包指令配置，提供一个入口。

需要一台mac osx的环境。

