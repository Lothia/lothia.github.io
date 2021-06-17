---
layout: post
title: "Temporary solution for Fedora 32 stuck at Starting Switch root"
tags: [fedora, fedora32, dracut]
comments: false
---

My problem was about dracut's new bluetooth module. 

Disable it with by creating a dot conf file in '/etc/dracut.conf.d' directory with this content 'omit_dracutmodules+=" bluetooth "' [*](https://github.com/dracutdevs/dracut/issues/1521#issuecomment-855325340)

You can follow the issue [here](https://github.com/dracutdevs/dracut/issues/1521).

This is the packece with dracut bug 'dracut-054-12.git20210521.fc34.x86_64.rpm', you can also solve this issue by downgrading dracut.
