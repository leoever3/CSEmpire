1)homebrew

morningstar@Tianxiongs-MacBook-Pro ~ % brew doctor

zsh: command not found: brew

 

 

morningstar@Tianxiongs-MacBook-Pro ~ % export PATH=/opt/homebrew/bin:$PATH

 

 

 

 

https://apple.stackexchange.com/questions/410825/apple-silicon-port-all-homebrew-packages-under-usr-local-opt-to-opt-homebrew?newreg=516b14269faa4d5381822d639d65fca5

 

2)JDK

For the system Java wrappers to find this JDK, symlink it with

 sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk

 

openjdk is keg-only, which means it was not symlinked into /opt/homebrew,

because macOS provides similar software and installing this software in

parallel can cause all kinds of trouble.

 

If you need to have openjdk first in your PATH, run:

 echo 'export PATH="/opt/homebrew/opt/openjdk/bin:$PATH"' >> ~/.zshrc

 

For compilers to find openjdk you may need to set:

 export CPPFLAGS="-I/opt/homebrew/opt/openjdk/include"

 

3)

pwd present woring dictionary

 

 

 

4)sublime

morningstar@Tianxiongs-MacBook-Pro ~ % sudo mkdir -p -m 775 /usr/local/bin

morningstar@Tianxiongs-MacBook-Pro ~ % export PATH=$PATH:/usr/local/bin

morningstar@Tianxiongs-MacBook-Pro temp % sudo ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl /usr/local/bin/.

 

 

 

 

 

chsh -s /bin/bash

chsh -s /bin/zsh

 

 

 

 

删除不掉文件

rm -rf /your/path

 

移除用户名 人名

https://www.cnblogs.com/iamchinese/p/p4.html

 

 

**personal token**

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

 

https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

 

**SSH**

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh

 

 

personal token

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

some short cut

^ space/fn  change language

Command space spotlight search