# Handover, 2026-09-21 14:50, control room

**What.** The commit recording Yassir's three acceptances failed in the "AI Control
Tower" repo with "fatal: loose object 9a854bf... is corrupt". Diagnosed and completed
without repairing, deleting or re-creating anything.

**Diagnosis, from evidence.** 9a854bf was the commit object git had just written, at
18:43:22, 308 bytes. A moment later `git fsck --full` read it whole, as a dangling
commit: parent 0c7b32e (main), tree 350cdcb, identical to `git write-tree` of the
staged index, blobs identical to `git hash-object` of the three working files. So git
wrote the object through the shared folder, read it back before the write was fully
visible, saw a truncated file and aborted before moving main. A read-back race on the
VM-to-Mac mount, not corruption.

**What the control room did.** `git update-ref refs/heads/main 9a854bf 0c7b32e`, the old
value as a guard, so it would have refused had main moved. fsck clean after, on both
repos. Both work-chat clones fetch and see 9a854bf.

**Rule added to both work-chat prompts.** On "object is corrupt" right after a write:
run fsck; clean means retry once; not clean means stop and report; never delete, move or
repair a git object. The dangerous response to this error is a repair attempt, and a
work chat, seeing "corrupt", might try one.

**Pattern worth watching.** Today's three git oddities, stale locks, deletes refused
despite a grant, and this read-back race, all sit on the same shared folder between the
Claude VM and the Mac. The heartbeat itself runs on macOS and has not shown any of them.
If they recur, the answer is fewer git writes from the VM, not more retries.

**Read first next time.** this file, then 2026-09-21-1445-runner-installed-designs-accepted.md.
