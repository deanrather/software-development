# Merge Conflict Resolution

If merging a topic branch into a version branch causes a conflict, eg:
In these examples, `1.2` is the version branch, `A` and `B` have already been merged in, and we're trying to merge in C.

    git checkout 1.2
    git merge A
    git merge B                     
    git merge C                     # Conflict!
    git reset --hard                # Cancels the merge of C into 1.2

It is assumed that `1.2`, `A`, `B`, and `C` all have `1.1` (latest production release) merged in.
It is unknown at this point wether `C` conflicts with `A` or `B`.
There are multiple ways to resolve this.

## Fixing the conflict between the Topic Branch and the Version Branch

### Make the version branch a dependency

Pro's: Quick & Easy
Con's: Pollutes your topic branch with all of the other stuff in the release

    git checkout C
    git merge 1.2                  # Conflict!
    # fix the conflict

### Fix the conflict on the Version Branch

Pro's: Quick & Easy
Con's: Makes the Version Branch more complicated to rebuild

    git checkout 1.2
    git merge C                     # Conflict!
    # fix the conflict
    # add fix to tag card

## Fixing the conflict between the Topic Branch and the conflicting Topic Branch

Determine the conflicting topic branch using a temporary merge testing branch.

    git checkout C
    git checkout -b C-merge-test
    git merge A                     # It's fine
    git merge B                     # Conflict!
    git checkout C
    git branch -D C-merge-test
    
We have determined that it is `B` that fails to merge with `C`

## Make This Branch Include the other Branch

    git checkout C
    git merge B                     # Conflict!
    # fix the conflict

## Make the Other Branch Include This Branch

    git checkout B
    git merge C                     # Conflict!
    # fix the conflict

## Prevent the Conflict

Pro's: Clean
Con's: Difficult & Timely

    git checkout C
    git merge B                     # Conflict!
    # Look at the conflict source
    git reset --hard                # Cancel the merge of B into C
    # Modify the code
    git merge B                     # Re-attempt the merge
