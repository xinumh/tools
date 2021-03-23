# 代码统计

```shell
git log --since=2020-11-01 --until=2020-12-03 --author="hx" --pretty=tformat: --numstat | gawk '{ add += $1 ; subs += $2 ; loc += $1 - $2 } END { printf "added lines: %s removed lines : %s total lines: %s\n",add,subs,loc }' -
```
