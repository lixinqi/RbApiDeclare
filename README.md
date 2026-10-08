# RbApiDeclare

RemoteBuddy 导出给规范的那两份东西：一个角色会哪些算子，和程序往会议目录里写的那几份数据写成什么。

```
rb_api/
    actor_api.viba          actor 会哪些算子
    critic_api.viba         critic 会哪些算子
    assistant_api.viba      assistant 会哪些算子
    ticket.viba             一张单（Ticket）、一次尝试（TicketStage）、它的全部进度（TicketProgress）
                            写成什么，还有里面用的 datetime 和 AppendOnlyList 两个名字
```

**这是 rb 和规范两个仓库中间的那一份，两边都依赖它，它不依赖任何一边**：

* 规范（`RbNorm`）里工单和规则 `import` 这几个名字，跑的时候按 `$VIBA_PATH` 找过来；规范自己那份
  `api_declare` 文件写着它按哪一版写（一个 commit id）。
* 程序（`RemoteBuddy-core`）提供这些算子的实现，照 `ticket.viba` 拼单、读单；一张工单上记着这一趟按的
  是哪一版声明（`$handler_name2api_declare_repo_commit_id`）。

声明和实现分开，是因为两边改的频率不一样：算子多一个、实参换一个、单上多一个成员，动的是这里；谁把
它做出来，动的是各自那一边。声明一改，规范和实现都得跟着改——所以这里的增补要慢。

**只有接口和数据写成什么**。这里没有实现，也没有一个角色在会议里做的事：算子的实现分别在
`RemoteBuddy-core` 的 `tickets/actor.py`、`tickets/critic.py`、`tickets/assistant.py` 里，单子怎么读写
在 `tickets/ticket.py`、`tickets/progress.py` 里。

规范自己也能带一份 `<角色>_api.viba`（多一个角色）；和这里的名字撞上是不允许的，跑的时候当场报出来。
