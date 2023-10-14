# ETH Hangzhou Hackathon 项目提交说明

ETH Hangzhou Hackathon 的项目需要提交到本页，PR（Pull-Request）截止时间为 2023年10月16日 下午14:00（北京时间，UTC+8）。你需要在你的项目下更新以下内容:
1. 项目名称
2. 所选赛道（Public Goods，Layer2 Application，Zero Knowledge 主赛道三选一）
3. 项目图片（1张有代表性的图片，不要过长）
4. 简介
5. 队长和队员
6. 本项目在这次黑客松的目标
7. 黑客松前两日的进度
8. Demo 视频链接（可以是录屏或其他形式），可以选择的视频平台：[Youtube](https://youtube.com)，[Bilibili](https://bilibili.com)，[Loom](https://www.loom.com/)，视频长度不能超过3分钟，否则扣分。
9. 项目 github repo 链接
10. 声明未基于之前的项目, 如: 该项目是本次hackathon期间，从0到1开发的项目，完全原创。
11. 项目 Demo 链接（选填）

在截止时间前提交 PR，且包含前 10 项信息的项目，视为提交成功，否则不参与评奖。

评委将在2023年10月16日下午14-18点期间，根据以下4个维度对项目进行第一轮打分，每个赛道的前5名可以参加晚上19点的Demo Day：
1. 代码 🧱
2. 创新性 💡
3. Demo完整度 📝
4. 对以太坊生态的重要性 ♻️

进入Demo Day的每个项目有 5 分钟展示时间。


以ETH Beijing获奖项目SLOADS为例, 请参考以下格式提交PR:


# SLOADS

**1 项目名称**: SLOADS

**2 所选赛道**: Public Goods

**3 项目图片**:

![foundry](https://book.getfoundry.sh/images/foundry-banner.png)

**4 简介**: 

Foundry 是一个以太坊智能合约开发框架。SLOADS 项目准备给它添加一个 feature，能够非常方便检索智能合约里面的所有 storage slot，特别是动态数据结构的，如 Array，Map。基于此，开发者可以更加方便地深入探索链上智能合约的状态，比如查找某个 token 的所有持币地址。工作内容：需要修改 foundry，foundry-std 里面的 cheatcode，以及 foundry-evm。起因则是在完成[这个 ctf](https://quillctf.super.site/challenges/quillctf-challenges/slot-puzzle) 时遇到了问题。

**5 队长和队员**: 

队长: [@liquan.eth](https://github.com/flyq) 队友：[@jjjpy](https://github.com/jpy1000)    [@clouds](https://github.com/clouds56)

**6 本项目在这次黑客松的目标:**

目标：
1. 修改 Foundry，能够在使用 Foundry 模版的 solidity 项目中的 test 中使用新增的几个 cheatcode。cheatcode 能够按照参数要求返回所有 storage slots 相关的信息。
    ```solidity
    function startMappingRecording() external;
    function getMappingLength(address target, bytes32 slot) external returns (uint);
    function getMappingSlotAt(address target, bytes32 slot, uint256 idx) external returns (bytes32);
    function getMappingKeyOf(address target, bytes32 slot) external returns (uint);
    function getMappingParentOf(address target, bytes32 slot) external returns (bytes32);
    ```
2. 新建一个合约本地测试 toolkit，用于简化和合约交互的命令。
   1. 用可以读取其他任意语言生成的 abi，并发送合约，测试结果
   2. 强类型语言，但在编写过程中可以有更简易的类型转换
   3. 并根据合约 abi 的 Json 文件自动化转换输入命令的参数。

**7 黑客松前两日的进度**

- Day 0:
  - [x] 完成组队，GitHub org&repo 的新建：https://github.com/0xevm
  - [x] 细化任务：
    1. 确定 cheatcode 的接口命名，并获取到对应的 function signature。
    2. 给 revm 新增接口，能够提取此时的某个 Account（智能合约） 里面的 storage map 的 key。
    3. 修改 foundry，当检查到调用的地址是 `CHEATCODE_ADDRESS`，且 function signature 满足条件时，调用底层的 revm 的新增接口，将结果（index 的 bytes 数组）返回。
    4. Option，在前面的基础上，建立 index bytes 和 map 的联系，比如对于 Map1 和 Map2，能够知道某个某个 slot 里面的数据是属于哪个 map 的哪个 key，需要 修改 revm 来在执行时记录一些 Metadata
    5. Option，将运行后的 evm 状态建立 snapshot，并存储为 json 文件，然后使用 forge inspect 时传入状态，获取此时所有的 storage layout。
    6. Option，在前面的基础上，给 forge test --debug 新增 storage layout，方便开发在逐步调试时能够看到 bytecode 的变化。
  - [x] 查看 foundry 文档，以及源码，确定修改路径。
- Day 1:
  - [x] 完成任务 1-4.
  - [x] 新建一个 toolkit，并根据合约 abi 的 Json 文件自动化转换输入命令的参数。
  - [x] 完成 team info 以及视频录制等。

**8 视频链接:**

https://www.bilibili.com/video/BV1LT411x72Q/

**9 项目 github repo 链接:**

所有代码都在

https://github.com/0xevm


**10 是否基于之前的项目:**

该项目是本次hackathon期间，从0到1开发的项目，完全原创。

**24.11 项目 Demo 链接（选填）:**
https://github.com/0xevm/sloads_demo#sloads-demo----