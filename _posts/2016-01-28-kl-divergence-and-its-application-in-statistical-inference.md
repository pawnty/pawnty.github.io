---
layout: post
title: KLɢ�ȼ�����ͳ��ѧϰ�е�Ӧ��
description: "����KLɢ�ȵĶ�������ʣ��Լ�EM�㷨������ƶϺ�"
modified: 2016-01-28
tags: [sample post]
categories: [Machine Learning]
---

##����

KLɢ�ȣ�Kullback Leibler Divergence���ֳ�����أ�Relative Entropy��������Ϣ�������ڱ�ʾ���ø���$p$�����ű�����������ʵ����Ϊ$q$����������Ҫ�Ķ�����Ϣ�������Ķ���ʽΪ
$$D(p||q)=-\int p(x)\ln\frac{q(x)}{p(x)}dx.$$

�����أ�entropy���Ǵ���$p$����Ҫ����С��Ϣ������֪$D(p||q)\ge 0$����һ��Ҳ���ɽ�ɭ����ʽ�õ���$$-\int p(x)\ln\frac{q(x)}{p(x)}dx\ge-\ln(\int p(x)\frac{q(x)}{p(x)}dx)=-\ln 1=0.$$������$-\ln(\cdot)$��͹������
