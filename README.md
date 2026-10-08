# RbApiDeclare

RemoteBuddy 导出给规范的那几个接口：一个角色会哪些算子，写在这里的 viba 声明里。

```
rb_api/
    actor_api.viba          actor 会哪些算子
    critic_api.viba         critic 会哪些算子
    assistant_api.viba      assistant 会哪些算子
```

**这是 rb 和规范两个仓库中间的那一份，两边都依赖它，它不依赖任何一边**：

* 规范（`RbNorm`）里工单和规则 `import` 这几个名字，跑的时候按 `$VIBA_PATH` 找过来；规范自己那份
  `api_declare` 文件写着它按哪一版写（一个 commit id）。
* 程序（`RemoteBuddy-core`）提供这些算子的实现，一张工单上记着这一趟按的是哪一版声明
  （`$handler_name2api_declare_repo_commit_id`）。

声明和实现分开，是因为两边改的频率不一样：算子多一个、实参换一个，动的是这里；谁把它做出来，动的是
各自那一边。声明一改，规范和实现都得跟着改——所以这里的增补要慢。

**只有接口**。这里没有实现，也没有一个角色在会议里做的事：算子的实现分别在 `RemoteBuddy-core` 的
`tickets/actor.py`、`tickets/critic.py`、`tickets/assistant.py` 里。

规范自己也能带一份 `<角色>_api.viba`（多一个角色）；和这里的名字撞上是不允许的，跑的时候当场报出来。
