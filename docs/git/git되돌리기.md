# git 되돌리기



## git reset

reset은 해당 시점으로 되돌아갑니다.
돌아가려는 커밋으로 레포지토리는 재설정되고, 해당 커밋 이후의 커밋 히스토리는 모두 삭제됩니다.

```
$ git reset --{옵션} {되돌아가려는 커밋 hash}
```

옵션으로는 대표적으로 hard, soft, mixed가 있습니다.
hard는 자주 써봐서 익숙하고..

### soft

soft는 hard와 마찬가지로 커밋 히스토리는 모두 삭제됩니다.

하지만 삭제되었던 내용들이 스테이징된 상태로 남아있습니다.

따라서 바로 commit을 하게되면 reset했던걸 취소(?)하는 효과를 볼 수 있습니다.

(단, commit message는 유지할 수 없고, 1개로 줄어드네요)

### mixed

옵션 default값입니다.

마찬가지로 커밋 히스토리는 모두 삭제됩니다.

하지만 아무것도 스테이징되어있지않습니다.



## git revert

revert는 해당 커밋만 삭제시킵니다.

그리고 commit history에 revert했다는 사실을 남깁니다.

보통, 원격 저장소에 push를 한 상태일때에는 reset을 사용하기보다는 revert를 사용한다고 합니다!

```
$ git revert {되돌릿 커밋 hash}
```

또한 범위를 주어서 여러개를 선택할 수 있습니다.

```
$ git revert {되돌릿 커밋 hash1.. 되돌릿 커밋 hash2}
```

