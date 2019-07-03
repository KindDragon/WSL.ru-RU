---
title: Вопросы и ответы по WSL 2
description: Часто задаваемые вопросы о подсистеме Windows для Linux 2
keywords: BashOnWindows, bash, wsl, wsl2, windows, подсистема windows для linux, windowssubsystem, ubuntu, debian, suse, windows 10, установка
author: mscraigloewen
ms.author: mscraigloewen
ms.date: 05/30/2019
ms.topic: article
ms.assetid: 7afaeacf-435a-4e58-bff0-a9f0d75b8a51
ms.custom: seodec18
ms.openlocfilehash: 84805278abaeb6334c662e1dfab1bced3e0ddb0b
ms.sourcegitcommit: bb88269eb37405192625fa81ff91162393fb491f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67038094"
---
# <a name="wsl-2-faq"></a>ЧАСТО ЗАДАВАЕМЫЕ ВОПРОСЫ О WSL 2

Ниже приведен список часто задаваемые вопросы (FAQ) о подсистеме Windows для Linux 2.

## <a name="does-wsl-2-use-hyper-v-will-it-be-available-on-windows-10-home"></a>Используется ли WSL 2 Hyper-V? Он будет доступен в Windows 10 Домашняя?

WSL 2 будут доступны во всех номерах SKU где WSL сейчас доступна, включая Windows 10 Домашняя.

Последняя версия WSL использует архитектуру Hyper-V его виртуализации. Эта архитектура будут доступны в дополнительный компонент, который представляет собой подмножество компонент Hyper-V. Это необязательный компонент, будут доступны во всех номерах SKU. Вы сможете узнать больше о эта возможность скоро поближе к выпуску WSL 2.

## <a name="what-will-happen-to-wsl-1-will-it-be-abandoned"></a>Что произойдет с WSL 1? Будет его брошенным?

В настоящее время у нас есть не планируем отказаться от WSL 1. Можно запустить WSL 1 и WSL 2 дистрибутивов рядом друг с другом и можно обновить и понизить любого дистрибутива в любое время. Добавление WSL 2 в качестве новой архитектуры представляется более эффективную платформу для команды WSL для предоставления функций, которые делают WSL удивительные способ запустить среду Linux в Windows.

## <a name="will-i-be-able-to-run-wsl-2-and-other-3rd-party-virtualization-tools-such-as-vmware-or-virtualbox"></a>Я смогу выполнять WSL 2 и других сторонних виртуализации средств VMware или VirtualBox?

Некоторые сторонние приложения не может работать при использовании Hyper-V, это означает, что они не смогут при включении WSL 2. К сожалению, это включает ли VMware и версии VirtualBox до VirtualBox 6 (VirtualBox 6.0.0, выпущенный в декабре 2018 [теперь поддерживает Hyper-V как базовая резервная выполнения на узле Windows] [ 1]!)

Мы изучаем способов, позволяющих устранить эту проблему. Например, мы предоставляем набор API, вызываемых [платформа низкоуровневой оболочки] [ 2] , виртуализации сторонних поставщиков можно использовать для обеспечения совместимости с Hyper-V программного обеспечения Это позволяет приложениям использовать архитектуру Hyper-V для их эмуляции, например [эмулятор Android Google][3], и, и VirtualBox, 6 и более поздних версий, которая теперь она совместима с Hyper-V.

## <a name="can-i-access-the-gpu-in-wsl-2-are-there-plans-to-increase-hardware-support"></a>Получить доступ к GPU в WSL 2? Планируется ли увеличить аппаратной поддержки?

В начальными выпусками доступ к оборудованию WSL 2 Поддержка будет ограничена, например: вы не сможете доступа к GPU, последовательный или USB. Однако добавление улучшения поддержки устройства велико в нашу невыполненную работу, как откроется многие дополнительные варианты использования для разработчиков, которым требуется взаимодействовать с этими устройствами. В то же время вы всегда можете использовать WSL 1, который имеет последовательный порт и доступа USB. . Следите за этот блог и WSL члены команды в Twitter для получения последних сведений о последних возможностях, ожидаемых в insider сборок и обратиться к Присылайте ваши отзывы о каких устройств, которые вы хотите взаимодействовать с!

## <a name="will-wsl-2-be-able-to-use-networking-applications"></a>WSL 2 смогут использовать сетевые приложения?

Да, в целом сети приложениях будет быстрее и лучше, поскольку у нас есть полный системный вызов совместимости. Тем не менее новая архитектура использует виртуализованные сетевые компоненты. Это означает, что в первоначальных предварительных сборок WSL 2 будет вести себя подобно тому к виртуальной машине, например: WSL 2 будет иметь разные IP-адреса хост-компьютере. Мы стремимся сделать WSL 2 вы так же, как WSL 1 и включающий в себя улучшению нашей сети истории. Мы планируем добавить улучшения сразу же после можно получить, например для доступа к всех сетевых приложений из Linux или Windows, с помощью localhost. Будет исправлена Дополнительные сведения о наших сетевых истории и усовершенствования, как мы используем подход выпуска WSL 2.

## <a name="can-i-run-wsl-2-in-a-virtual-machine"></a>Можно ли запускать WSL 2 на виртуальной машине?

Да! Необходимо убедиться, что виртуальная машина имеет вложенные виртуализация включена. Эту функцию можно включить в Hyper-V, выполнив следующую команду в окне PowerShell с правами администратора:

`Set-VMProcessor -VMName <VMName> -ExposeVirtualizationExtensions $true`

Обязательно замените "&lt;VMName&gt;" с именем виртуальной машины.

 [1]: https://www.virtualbox.org/wiki/Changelog-6.0
 [2]: https://docs.microsoft.com/en-us/virtualization/api/
 [3]: https://devblogs.microsoft.com/visualstudio/hyper-v-android-emulator-support/