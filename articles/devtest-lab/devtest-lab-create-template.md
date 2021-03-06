---
title: VM을 만드는 Azure DevTest Labs 사용자 지정 이미지 관리 | Microsoft Docs
description: VHD 파일 또는 DevTest Lab의 기존 VM에서 사용자 지정 이미지를 만드는 방법 알아보기
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''

ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: tarcher

---
# VM을 만드는 Azure DevTest Labs 사용자 지정 이미지 관리
Azure DevTest Labs에서 사용자 지정 이미지를 사용하면 모든 필수 소프트웨어가 대상 컴퓨터에 설치될 때까지 기다리지 않고도 VM을 빠르게 만들 수 있습니다. 사용자 지정 이미지를 사용하면 VHD 파일에 필요한 모든 소프트웨어를 미리 설치하고 VHD 파일을 사용하여 VM을 만들 수 있습니다. 소프트웨어가 이미 설치되어 있으므로 VM 생성 시간이 훨씬 단축됩니다. 또한 VM에서 사용자 지정 이미지를 만든 다음 해당 사용자 지정 이미지에서 VM을 만듭니다.

이 문서에서는 다음 방법을 설명합니다.

* 사용자 지정 이미지에서 VM을 만들 수 있도록 [VHD 파일에서 사용자 지정 이미지 만들기](#create-a-custom-image-from-a-vhd-file)
* 빠른 VM 복제를 위해 [VM에서 사용자 지정 이미지 만들기](#create-a-custom-image-from-a-vm)

## VHD 파일에서 사용자 지정 이미지 만들기
이 섹션에는 VHD 파일에서 사용자 지정 이미지를 만드는 방법이 나와 있습니다. 이 섹션의 모든 단계를 수행하려면 올바른 VHD 파일에 액세스할 수 있어야 합니다.

1. [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.
2. **서비스 더 보기**를 선택한 후 목록에서 **DevTest Lab**을 선택합니다.
3. 랩 목록에서 원하는 랩을 탭합니다.
4. 랩의 블레이드에서 **구성**을 선택합니다.
5. 랩 **구성** 블레이드에서 **사용자 지정 이미지**를 선택합니다.
6. **사용자 지정 이미지** 블레이드에서 **+ 사용자 지정 이미지**를 선택합니다.
   
    ![사용자 지정 이미지 추가](./media/devtest-lab-create-template/add-custom-image.png)
7. 사용자 지정 이미지의 이름을 입력합니다. 이 이름은 VM을 만들 때 기본 이미지 목록에 표시됩니다.
8. 사용자 지정 이미지에 대한 설명을 입력합니다. 이 설명은 VM을 만들 때 기본 이미지 목록에 표시됩니다.
9. **VHD 파일**을 선택합니다.
10. 목록에 없는 VHD 파일에 액세스하려면 [VHD 파일 업로드](#upload-a-vhd-file) 섹션의 지침에 따라 추가한 후 완료되면 여기로 돌아옵니다.
11. 원하는 VHD 파일을 선택합니다.
12. **확인**을 선택하여 **VHD 파일** 블레이드를 닫습니다.
13. **OS 구성**을 선택합니다.
14. **OS 구성** 탭에서 **Windows** 또는 **Linux**를 선택합니다.
15. **Windows**가 선택되면 확인란을 통해 컴퓨터에서 *Sysprep* 이 실행되었는지를 지정합니다.
16. **확인**을 선택하여 **OS 구성** 블레이드를 닫습니다.
17. **확인**을 선택하여 사용자 지정 이미지를 만듭니다.
18. [다음 단계](#next-steps) 섹션으로 이동합니다.

### VHD 파일 업로드
사용자 지정 이미지를 추가하려면 VHD 파일에 액세스할 수 있어야 합니다.

1. **VHD 파일** 블레이드에서 **PowerShell을 사용하여 VHD 파일 업로드**를 선택합니다.
   
    ![이미지 업로드](./media/devtest-lab-create-template/upload-image-using-psh.png)
2. 다음 블레이드는 Azure 구독에 VHD 파일을 업로드하는 PowerShell 스크립트를 수정하고 실행하기 위한 지침을 표시합니다. **참고:** 이 프로세스는 VHD 파일 크기 및 연결 속도에 따라 시간이 오래 걸릴 수 있습니다.

## VM에서 사용자 지정 이미지 만들기
VM이 이미 구성되어 있는 경우 VM에서 사용자 지정 이미지를 만들고 나중에 해당 사용자 지정 이미지를 다른 동일한 VM을 만드는 데 사용할 수 있습니다. 다음 단계에서는 VM에서 사용자 지정 이미지를 만드는 방법을 보여 줍니다.

1. [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.
2. **서비스 더 보기**를 선택한 후 목록에서 **DevTest Lab**을 선택합니다.
3. 랩 목록에서 원하는 랩을 탭합니다.
4. 랩의 블레이드에서 **내 가상 컴퓨터**를 선택합니다.
5. **내 가상 컴퓨터** 블레이드에서 사용자 지정 이미지를 만들 VM을 선택합니다.
6. VM의 블레이드에서 **사용자 지정 이미지 만들기(VHD)**를 선택합니다.
   
    ![사용자 지정 이미지 만들기 메뉴 항목](./media/devtest-lab-create-template/create-custom-image.png)
7. **이미지 만들기** 블레이드에서 사용자 지정 이미지에 대한 이름 및 설명을 입력합니다. 이 정보는 VM을 만들 때 기본 목록에 표시됩니다.
   
    ![사용자 지정 이미지 만들기 블레이드](./media/devtest-lab-create-template/create-custom-image-blade.png)
8. sysprep이 VM에서 실행되었는지 여부를 선택합니다. sysprep이 VM에서 실행되지 않은 경우 이 사용자 지정 이미지에서 VM을 만들 때 sysprep을 실행할지를 지정합니다.
9. 완료했으면 **확인**을 선택하여 사용자 지정 이미지를 만듭니다.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## 관련 블로그 게시물
* [사용자 지정 이미지 또는 수식?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
* [Azure DevTest Labs 간의 사용자 지정 이미지 복사](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

## 다음 단계
VM을 만들 때 사용할 사용자 지정 이미지를 추가했으면 다음 단계는 [랩에 VM을 추가](devtest-lab-add-vm-with-artifacts.md)하는 것입니다.

<!---HONumber=AcomDC_0907_2016-->