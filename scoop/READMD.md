### windows install pnpm use git-bash
curl -fsSL https://get.pnpm.io/install.sh | sh -

### [install scoop](https://scoop.sh/)
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression

### install bun
scoop install bun

### ripgrep
scoop install ripgrep

scoop install main/python
scoop install main/oh-my-posh

scoop install main/composer

#### [rsync](https://scicomp.aalto.fi/scicomp/rsynconwindows/)

### cargo tauri cli
cargo install tauri-cli --version "^2.0.0" --locked

### install tauri for android
rustup target add aarch64-linux-android armv7-linux-androideabi i686-linux-android x86_64-linux-android

### [install z-lua](https://github.com/skywind3000/z.lua/blob/master/README.cn.md)

scoop install z-lua

```md
# 检查配置文件的路径
$profile
# 检查在系统上是否创建了 PowerShell 配置文件
test-path $profile
# 如果没有创建的话，创建一下
new-item -path $profile -itemtype file -force
# 使用记事本打开配置文件
notepad $profile

# 将以下内容写入打开的配置文件

# z-lua
Invoke-Expression (& { (lua /path/to/z.lua --init powershell) -join "`n" })
# j 别名到 z
Set-Alias j z
```
