---
title: "Architecture - Error handling"
tags: [architecture]
keywords: architecture, error, exception
sidebar: developer_guide_sidebar
permalink: developer_guide_architecture_error_handling.html
folder: developer_guide
---


## Exceptions

### Base classes

1. All custom platform exceptions should inherit from [AnchorCheckedException](https://github.com/anchoranalysis/anchor/blob/master/anchor-core/src/main/java/org/anchoranalysis/core/error/AnchorCheckedException.java) and [AnchorRuntimeException](https://github.com/anchoranalysis/anchor/blob/master/anchor-core/src/main/java/org/anchoranalysis/core/error/AnchorRuntimeException.java).
2. Two additional abstract classes [AnchorFriendlyCheckedException](https://github.com/anchoranalysis/anchor/blob/master/anchor-core/src/main/java/org/anchoranalysis/core/error/friendly/AnchorFriendlyCheckedException.java) and [AnchorFriendlyRuntimeException](https://github.com/anchoranalysis/anchor/blob/master/anchor-core/src/main/java/org/anchoranalysis/core/error/friendly/AnchorFriendlyRuntimeException.java) indicate exceptions which are guaranteed to have either:
  * either a user-friendly error message describing whats going wrong.
  * simply nest another exception, with a blank `""` message.

### Design contract of throwing the exceptions
By throwing a **friendly** exception, the developer promises that simply displaying this exception (and the messages of its nested causes) are sufficient to explain the error to the end-user.

By throwing a **non-friendly**, this implies that more information (e.g. a stack trace) should be shown to the user, so they can figure out what went wrong.

### Longer-term progression towards friendly-exceptions

As stack-traces are ugly to display to the end-user, it is planned over time:

1. Turn more custom-exceptions into *friendly* exceptions.
2. Eliminate friendly-exceptions with blank `""` messages (containing only a nested exception). Insist on messages.

{% include links.html %}