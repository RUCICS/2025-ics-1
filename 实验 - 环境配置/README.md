# 实验前 - 环境配置

ICS I 共有 4 个 Lab，分别是 DataLab、BombLab、CacheLab 和 LinkLab。

这些 Lab 都需要在 Linux 环境下完成，因此需要先配置好实验环境。

## 1. 安装 WSL

### 1.1. 认识 WSL 和 Linux

Windows Subsystem for Linux (WSL) 是微软提供的一个在 Windows 上运行 Linux 的子系统。

你说，Windows 我知道是什么，但什么是 Linux？Linux 是一种开源的类 Unix 操作系统。你又要说了，
什么是操作系统？什么是开源的类 Unix 操作系统？

#### 1.1.1. 什么是操作系统？

生活中，我们说一个手机是 Android 系统或者 iOS 系统，说一台电脑是 Windows 系统或者 macOS 系统，这些 Android、iOS、Windows、macOS 都是操作系统。

安卓的 Apk 文件不能在 iOS 系统上运行，Windows 的 exe 文件不能在 macOS 上运行，ICS Labs 的程序也只能在 Linux 系统上运行，而不能直接在 Windows 上运行。之所以这样，是因为这些应用程序（Applications）需要操作系统（Operating System）提供的各种服务，而不同的操作系统提供的服务是不一样的。

![什么是操作系统？](.img/Devices_and_Computers_sm.webp)

关于操作系统具体是什么，这是一个很专业的问题。我们这里不深入探讨，只要能理解操作系统是介于硬件和应用程序之间的软件就可以了。

#### 1.1.2. “开源的类 Unix 操作系统”是什么意思？

我们知道，贝尔发明了电话，并创立了贝尔电话公司，贝尔电话公司后来演变为了我们耳熟能详的 AT&T 公司（American Telephone and Telegraph Company）。AT&T 作为最早的电信服务提供商，毫无疑问是计算机最早的商业使用者之一。当时的计算机主流是“批处理”（Batch Processing）系统，用户需要将任务（如穿孔卡片）提交给操作员，然后等待数小时甚至数天才能得到结果，对于 AT&T 这种大公司来说，显然无法接受这种效率。

为了解决该问题，AT&T 先后开发了 CTSS 和 Multics 操作系统，最终 Multics 由于过于复杂而失败了。Ken Thompson 和 Dennis Ritchie 这两位贝尔实验室的研究员按照 Multics 的思路，重新设计了一个更小更简单的操作系统，这就是 Unix 操作系统。

Unix 系统由于其简洁、稳定和强大，在 AT&T 内掀起了一场革命。职员只需要坐在被称为终端（Terminal）的电传打字机（Teletypewriter, TTY）前就可以方便的编辑文件，打错一个字就不得不重新打一整页的时代一去不复返了。工程师们也不再需要通过一个孔也不能打错的纸条来升级 AT&T 的那些复杂的电信控制程序。

但是，根据《1956年最终判决》，AT&T 作为一家电信公司，不能从事计算机业务，因此 Unix 系统被迫开源。Unix 的源代码被许多大学和研究机构使用和修改，衍生出了许多不同的版本（Version），如 BSD、System V 等。

![源远流长的 Unix 家族](.img/Unix_history-simple.svg.png)

在这种背景下，Andrew S. Tanenbaum 教授为了教学目的，开发了一个与 Unix 兼容但代码完全独立的迷你版 Unix，并将其命名为 Minix（Mini-Unix 的缩写）。Minix 的全部源代码随同他的教科书《操作系统：设计及实现》一同发布。

芬兰的一名21岁的计算机系学生 Linus Torvalds 在学习后对 Minix 的一些设计感到不满，于是在 1991 年，Linux 开始着手开发自己的内核。与此同时，由 Richard Stallman 发起的 GNU 项目也在如火如荼的推进，GNU 项目旨在开发一个完全自由的类 Unix 操作系统，让计算机用户从专业软件昂贵的授权中解放出来。GNU 项目开发了许多操作系统所需的工具和库，但始终缺少一个内核。Linus 和 GNU 项目的成员一拍即合，共同开发了一个完整的类 Unix 操作系统：GNU/Linux 操作系统，简称 Linux。

GNU/Linux 由于其开源、免费、稳定和强大，发展迅速，从一个小众的操作系统，逐渐发展成为服务器主流操作系统。与 Unix 不同，由于 Linux 的内核始终由 Linus 和一些核心开发者维护，Linux 内核并未分叉出多个版本。内核与不同系统软件的结合，形成了各种不同的 Linux 发行版（Distribution），如 Debian、Ubuntu、CentOS、Fedora 等。

![Linux 的象征标志是这只企鹅](.img/tux.jpg)

#### 1.1.3. 关于 WSL 和 Linux 环境

很长一段时间里，在 Windows 上运行 Linux 只能通过虚拟机（如 VirtualBox、VMware）或者双系统（Dual Boot）来实现。

虚拟机是一种神奇的技术，这种技术通过软件模拟出一台计算机的硬件，并在这台虚拟的计算机上运行操作系统。随着虚拟化技术的发展，虚拟机的性能越来越好，逐渐可以媲美物理机。但使用虚拟机安装 Linux 总归不是很方便，而且 Windows 上最强大的虚拟化软件 VMWare 并不是免费的，而开源的 VirtualBox 的易用性和性能都不如 VMWare。

2016 年，微软发布了 WSL 1，WSL 1 试图让 Windows 内核对这些程序表现的和 Linux 内核一样，但由于二者总有些微妙的差异，这种方式的效果并不好，很多 Linux 程序无法运行。

2019 年，微软发布了 WSL 2，WSL 2 利用 Windows 内置的 Hyper-V 虚拟化技术，在 Windows 上运行一个真正的 Linux 内核，这样就可以完美的运行 Linux 程序了。WSL 2 的性能也非常好，几乎和在物理机上运行 Linux 没有区别。

![WSL](.img/wsl-en.png)

我们课程中，由于大部分同学使用 Windows 系统，而我们的实验需要在 Linux 环境下完成，综合考虑易用性等因素，我们推荐大家使用 WSL 2 来配置 Linux 环境。但是，这并不意味着 WSL 是唯一的选择，如果你愿意使用传统的虚拟机来运行 Linux，也是可以的。再或者，你也可以使用双系统等方式，直接在物理机上运行 Linux。

对于 MacOS 用户来说，虽然 macOS 本身就是一个类 Unix 操作系统，但因为较新的 Mac 采用 Arm 芯片，而 GDB 等调试工具对 Arm 的支持并不好，所以有些实验可能无法完成。我们推荐 Mac 用户使用虚拟机，或通过下述的远程连接服务器的方式完成任务。

无论你是 Windows 用户还是 Mac 用户，如果想体验纯正的 Linux 环境和多用户环境，你可以通过 SSH 连接到我们提供的 Linux 服务器上完成实验任务。你需要向助教李甘（微信：nictheboy，手机：136 8158 2912 ，邮箱：<ligan@ruc.edu.cn>）申请一个用户。不过由于服务器上会有很多用户同时使用，性能可能会受到影响。但这依旧会是一段不错的体验，你可以体验一下计算机科学的前辈们是如何在公用的计算机上借助多用户操作系统的强大资源共享能力完成任务，不过这也会带来一些不便，需要你逐渐适应。

还有一些类似于上面讲的 WSL 1 的技术，如 Cygwin、MSYS2 等，通过软件方式在 Windows 上模拟 Linux 环境，但和 WSL 1 一样，这些方式并不完美。过去没有人尝试过用这些工具完成 ICS Labs 任务，但如果你愿意尝试，也是可以的。你可以把你的这些奇特的环境配置过程和结果分享到我们的论坛 [http://forum.rucics.tech](http://forum.rucics.tech)，通过这样的过程更好地了解计算机系统。

总之，你需要一个 Linux 环境来完成 ICS Labs 的任务。我们推荐 Windows 用户使用 WSL 2，Mac 用户使用虚拟机或服务器，但只要你愿意折腾而不嫌麻烦，任何方式都是可以的。助教团队愿意随时为你们提供技术支持。

### 1.2. WSL 2 安装步骤

## 2. 在 WSL 内安装 Git

## 3. 安装 VSCode 并连接 WSL
