---
title: "Hadoop 소개 - HDInsight의 Hadoop은 무엇입니까? | Microsoft Docs"
description: "HDInsight의 클라우드에서 Hadoop, 분산된 빅 데이터 처리 및 분석과 Hadoop 에코시스템의 구성 요소에 대해 소개합니다."
keywords: "빅 데이터 분석, Hadoop 소개, Hadoop이란, Hadoop 기술 스택, Hadoop 에코시스템"
services: hdinsight
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/21/2016
ms.author: cgronlun
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: cefda0778fed4ab8d502955dd8eae4bdac70a48e


---
# <a name="an-introduction-to-the-hadoop-ecosystem-on-azure-hdinsight"></a>Azure HDInsight의 Hadoop 에코시스템에 대한 소개
 이 문서는 Azure HDInsight, 해당 에코시스템 및 빅 데이터에 Hadoop에 대한 소개를 제공합니다. Hadoop 구성 요소, 일반적인 용어 및 빅 데이터 분석의 시나리오에 대해 알아봅니다.

## <a name="what-is-hadoop-on-hdinsight"></a>HDInsight의 Hadoop은 무엇입니까?
Hadoop은 컴퓨터의 클러스터에서 빅 데이터 집합의 분산 처리, 저장 및 분석을 위한 프레임워크인 오픈 소스 소프트웨어의 에코시스템을 가리킵니다. Azure HDInsight를 사용하면 **HDP(Hortonworks Data Platform)** 배포의 Hadoop 구성 요소를 클라우드에서 사용할 수 있고 높은 안정성 및 가용성을 가진 관리되는 클러스터를 배포하고 프로비전할 수 있습니다.  

Apache Hadoop은 원래 빅 데이터 처리를 위한 오픈 소스 프로젝트였습니다. Apache Hive, Apache HBase, Apache Spark 및 많은 기타 프로그램을 포함하는 Hadoop 기술 스택의 일부로 간주되는 관련된 소프트웨어 및 유틸리티는 다음과 같이 개발되었습니다. 자세한 내용은 [HDInsight의 Hadoop 에코시스템 개요](#overview)를 참조하세요.

## <a name="what-is-big-data"></a>빅 데이터란?
빅 데이터는 Twitter 피드의 텍스트, 산업 장비의 센서 정보, 웹사이트의 고객 검색 및 구매 관련 정보에 이르기까지 모든 디지털 정보의 본문을 설명하며 기록 데이터, 즉 저장된 데이터일 수도 있고 실시간 데이터, 즉 원본에서 직접 스트리밍되는 데이터일 수도 있습니다. 빅 데이터는 갈수록 많은 양이 다양한 형식으로 더 빠르게 수집되고 있습니다.

실행 가능한 인텔리전스 또는 의견을 제공하는 빅 데이터의 경우 관련 데이터를 수집하고 올바로 질문해야 합니다. 또한 데이터에 액세스 가능하고 데이터를 정리, 분석하고 유용한 방식으로 표시하도록 합니다. 이 경우 HDInsight의 Hadoop에 대한 빅 데이터 분석이 유용할 수 있습니다.

## <a name="a-nameoverviewaoverview-of-the-hadoop-ecosystem-in-hdinsight"></a><a name="overview"></a>HDInsight의 Hadoop 에코 시스템 개요
HDInsight는 빅 데이터 분석을 위해 빠르게 확장되는 Apache Hadoop 기술 스택인 Microsoft Azure를 기반으로 하는 클라우드 구현입니다. Apache Spark, HBase, Storm, Pig, Hive, Sqoop, Oozie, Ambari 등의 구현이 포함됩니다. 또한 HDInsight는 Power BI, Excel, SQL Server Analysis Services 및 SQL Server Reporting Services 등의 BI(비즈니스 인텔리전스) 도구와도 통합됩니다.

### <a name="hadoop-hbase-spark-storm-and-customized-clusters"></a>Hadoop, HBase, Spark, Storm 및 사용자 지정된 클러스터
HDInsight는 Apache Hadoop, Spark, HBase 또는 Storm에 대한 클러스터 구성을 제공합니다. 또는 [스크립트 동작으로 클러스터를 사용자 지정할](hdinsight-hadoop-customize-cluster-linux.md)수 있습니다.

* **Hadoop**: 데이터를 병렬로 처리하고 분석하도록 [HDFS](#hdfs)를 통해 신뢰할 수 있는 데이터 저장소와 간단한 [MapReduce](#mapreduce) 프로그래밍 모델을 제공합니다.
* **<a target="_blank" href="http://spark.apache.org/">Apache Spark</a>**: 메모리 내 처리를 지원하여 빅 데이터 분석 응용 프로그램, SQL의 Spark 작업, 스트리밍 데이터 및 기계 학습의 성능을 향상하는 병렬 처리 프레임워크입니다. 자세한 내용은 [개요: HDInsight에서 Apache Spark란?](hdinsight-apache-spark-overview.md)
* **<a target="_blank" href="http://hbase.apache.org/">HBase</a>**: 구조화되지 않은/반구조화된 대량 데이터(잠재적으로 수십억 개의 행과 수십억 개의 열로 구성됨)에 대해 임의 액세스 및 강력한 일관성을 제공하는 Hadoop 기반의 NoSQL 데이터베이스입니다. [HDInsight의 HBase 개요](hdinsight-hbase-overview.md)를 참조하세요.
* **<a  target="_blank" href="https://storm.incubator.apache.org/">Apache Storm</a>**: 대규모 데이터 스트림을 빠르게 처리하기 위한 분산형 실시간 계산 시스템으로입니다. HDInsight에서 관리 클러스터로 제공됩니다. [Storm 및 Hadoop을 사용하여 실시간 센서 데이터 분석](hdinsight-storm-sensor-data-analysis.md)을 참조하세요.

### <a name="example-customization-scripts"></a>예제 사용자 지정 스크립트
스크립트 동작은 클러스터가 프로비전되는 동안 실행되는 스크립트이며 클러스터에 추가 구성 요소를 설치하는 데 사용할 수 있습니다. Linux 기반 클러스터의 경우에는 Bash 스크립트가 해당합니다.

다음은 HDInsight 팀에서 제공하는 예제 스크립트입니다.

* [Hue](hdinsight-hadoop-hue-linux.md): 클러스터를 조작하는 데 사용되는 웹 응용 프로그램 집합입니다. Linux 클러스터에만 해당합니다.
* [Giraph](hdinsight-hadoop-giraph-install-linux.md): 사물 또는 사람 간의 관계를 모델링하기 위한 그래프 처리입니다.
* [R](hdinsight-hadoop-r-scripts-linux.md): 기계 학습에서 사용되는 통계 계산을 위한 오픈 소스 언어 및 환경입니다.
* [Solr](hdinsight-hadoop-solr-install-linux.md): 데이터에 대해 전체 텍스트 검색을 허용하는 엔터프라이즈급 검색 플랫폼입니다.

사용자 고유의 스크립트 작업 개발에 대한 정보는 [HDInsight를 사용하여 스크립트 작업 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.

## <a name="what-are-the-hadoop-components-and-utilities"></a>Hadoop 구성 요소와 유틸리티란?
다음 구성 요소와 유틸리티가 HDInsight 클러스터에 포함됩니다.

* **[Ambari](#ambari)**: 클러스터 프로비전, 관리, 모니터링 및 유틸리티.
* **[Avro](#avro)**(Microsoft .NET Library for Avro): Microsoft .NET 환경을 위한 데이터 직렬화.
* **[Hive 및 HCatalog](#hive)**: 쿼리 및 테이블 및 저장소 관리 계층과 같은 구조적 쿼리 언어(SQL).
* **[Mahout](#mahout)**: 응용 프로그램을 학습하는 확장 가능한 컴퓨터의 경우.
* **[MapReduce](#mapreduce)**- Hadoop 분산 처리 및 리소스 관리를 위한 레거시 프레임워크. 차세대 리소스 프레임워크인 [YARN](#yarn)을 참조하세요.
* **[Oozie](#oozie)**- 워크플로 관리.
* **[Phoenix](#phoenix)**: HBase를 통한 관계형 데이터베이스 계층.
* **[Pig](#pig)**- MapReduce 변환을 위한 간단한 스크립팅.
* **[Sqoop](#sqoop)**-데이터 가져오기 및 내보내기.
* **[Tez](#tez)**: 데이터 집약적인 프로세스를 대규모로 효율적으로 실행할 수 있게 합니다.
* **[YARN](#yarn)**: Hadoop 코어 라이브러리의 일부 및 차세대 MapReduce 소프트웨어 프레임워크.
* **[ZooKeeper](#zookeeper)**- 분산 시스템의 프로세스 조정.

> [!NOTE]
> 특정 구성 요소 및 버전 정보에 대한 자세한 내용은 [HDInsight의 Hadoop 구성 요소, 버전 관리 및 서비스 제품][component-versioning]을 참조하세요.
> 
> 

### <a name="a-nameambariaambari"></a><a name="ambari"></a>Ambari
Apache Ambari는 Apache Hadoop 클러스터를 프로비전하고 관리 및 모니터링합니다. Hadoop의 복잡성을 숨기고 클러스터 작업을 단순화하는 직관적인 연산자 도구 모음 및 강력한 API 집합이 포함되어 있습니다. Linux 기반 HDInsight 클러스터는 Ambari 웹 UI와 Ambari REST API 둘 다 제공하는 반면 Windows 기반 클러스터는 REST API의 하위 집합을 제공합니다. HDInsight 클러스터의 Ambari 뷰는 플러그 인 UI 기능을 허용합니다.

[Ambari를 사용하여 HDInsight 클러스터링 관리](hdinsight-hadoop-manage-ambari.md)(Linux만 해당), [Ambari API를 사용하여 HDInsight에서 Hadoop 클러스터 모니터링](hdinsight-monitor-use-ambari-api.md) 및 <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">Apache Ambari API 참조</a>를 참조하세요.

### <a name="a-nameavroaavro-microsoft-net-library-for-avro"></a><a name="avro"></a>Avro (Microsoft .NET Library for Avro)
Microsoft .NET Library for Avro는 Microsoft .NET 환경용 직렬화를 위한 Apache Avro 압축 이진 데이터 교환 형식을 구현합니다. It uses <a target="_blank" href="http://www.json.org/">JSON(JavaScript Object Notation)</a>을 사용하여 언어 상호 운용성을 따르는 언어 중립적 스키마를 정의합니다. 따라서 특정 언어로 직렬화된 데이터를 다른 언어에서 읽을 수 있습니다. <a target=_"blank" href="http://avro.apache.org/docs/current/spec.html">Apache Avro 사양</a>에서 형식에 대한 자세한 정보를 찾을 수 있습니다.
Avro 파일의 형식은 분산된 MapReduce 프로그래밍 모델을 지원합니다. 파일은 "분할 가능"하므로 파일에서 임의의 지점을 찾고 특정 블록부터 읽기 시작할 수 있습니다. 해당 방법은 [Avro용 Microsoft .NET Library로 데이터 직렬화](hdinsight-dotnet-avro-serialization.md)를 참조하세요.

### <a name="a-namehdfsahdfs"></a><a name="hdfs"></a>HDFS
HDFS(Hadoop Distributed File System)는 MapReduce 및 YARN과 함께 Hadoop 에코시스템의 핵심 구성 요소인 분산 파일 시스템이자 HDInsight의 Hadoop 클러스터용 표준 파일 시스템입니다.

### <a name="a-namehiveahive-hcatalog"></a><a name="hive"></a>Hive & HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a>는 Hadoop을 기반으로 작성되는 데이터 웨어하우스 소프트웨어로, HiveQL이라는 SQL 스타일 언어를 사용하여 분산 저장소에서 대형 데이터 집합을 쿼리 및 관리하는 데 사용할 수 있습니다. Pig와 마찬가지로 Hive는 MapReduce 위에 있는 추상화 계층입니다. Hive를 실행하면 일련의 MapReduce 작업을 쿼리합니다. 개념상 Hive는 Pig보다 관계형 데이터베이스 관리 시스템에 더 가까우므로 보다 구조적인 데이터에 사용하기에 적합합니다. 구조화되지 않은 데이터의 경우에는 Pig가 더 적합합니다. [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)을 참조하세요.

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a>는 사용자에게 데이터의 관계형 뷰를 표시하는 Hadoop의 테이블 및 저장소 관리 계층입니다. HCatalog에서, Hive SerDe(serializer-deserializer)를 쓸 수 있는 모든 형식으로 파일을 읽고 쓸 수 있습니다.

### <a name="a-namemahoutamahout"></a><a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a>는 Hadoop에서 실행되는 기계 학습 알고리즘의 확장 가능한 라이브러리입니다. 기계 학습 응용 프로그램은 통계 원칙을 사용하여 시스템이 데이터로부터 학습을 하고 이전 결과를 사용해 이후 동작을 결정하도록 가르칩니다. [Hadoop에서 Mahout를 사용하여 영화 추천 생성](hdinsight-mahout.md)을 참조하세요.

### <a name="a-namemapreduceamapreduce"></a><a name="mapreduce"></a>MapReduce
MapReduce는 빅 데이터 집합을 병렬로 일괄 처리하는 응용 프로그램 작성용 Hadoop에 대한 레거시 소프트웨어 프레임워크입니다. 이 작업에서는 큰 데이터 집합을 분할한 다음 처리를 위해 데이터를 키-값 쌍으로 구성합니다.

[YARN](#yarn) 은 Hadoop 차세대 리소스 관리자 및 응용 프로그램 프레임워크로 MapReduce 2.0이라고 합니다. MapReduce 작업은 YARN에서 실행됩니다.

MapReduce에 대한 자세한 내용은 Hadoop Wiki에서 <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> 를 참조하세요.

### <a name="a-nameoozieaoozie"></a><a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a>는 Hadoop 작업을 관리하는 워크플로 코디네이션 시스템입니다. Hadoop 스택과 통합되며 MapReduce, Pig, Hive 및 Sqoop용 Hadoop 작업을 지원합니다. Java 프로그램이나 셸 스크립트와 같이 시스템에 특정한 작업을 예약하는 데에도 사용할 수 있습니다. [Hadoop과 함께 Oozie 사용](hdinsight-use-oozie.md)을 참조하세요.

### <a name="a-namephoenixaphoenix"></a><a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a>는 HBase를 기반으로 둔 관계형 데이터베이스 계층입니다. Phoenix는 사용자가 SQL 테이블을 직접 관리하고 쿼리할 수 있는 JDBC 드라이버를 포함합니다. Phoenix는 MapReduce를 사용하지 않고 쿼리 및 다른 문을 네이티브 NoSQL API로 변환하므로 NoSQL 저장소 위에서 더 빠른 응용 프로그램을 사용할 수 있습니다. [HBase 클러스터와 함께 Apache Phoenix 및 SQuirreL 사용](hdinsight-hbase-phoenix-squirrel.md)을 참조하세요.

### <a name="a-namepigapig"></a><a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a>는 Pig Latin이라는 단순한 스크립팅 언어를 사용하여 매우 큰 데이터 집합에 대해 복잡한 MapReduce 변환을 수행하는 데 사용할 수 있는 고급 플랫폼입니다. Pig는 Hadoop 내에서 실행되도록 Pig Latin 스크립트를 변환합니다. UDF(사용자 정의 함수)를 만들어 Pig Latin을 확장할 수 있습니다. [Hadoop과 함께 Pig 사용](hdinsight-use-pig.md)을 참조하세요.

### <a name="a-namesqoopasqoop"></a><a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a>은 Hadoop과 관계형 데이터베이스(예: SQL) 또는 기타 구조적 데이터 저장소 간에 대량 데이터를 최대한 효율적으로 전송하는 도구입니다. [Hadoop과 함께 Sqoop 사용](hdinsight-use-sqoop.md)을 참조하세요.

### <a name="a-nametezatez"></a><a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a>는 복잡하고 방향이 있는 일반 데이터 처리 그래프를 실행하는 Hadoop YARN에서 빌드된 응용 프로그램 프레임워크입니다. 대규모로 보다 효율적으로 실행되도록 Hive와 같은 데이터를 많이 사용하는 프로세스를 허용하는 MapReduce 프레임 워크에 대한 더 유연하고 강력한 후속 작업입니다. [Hive와 HiveQL에서"향상된 성능을 위해 Apache Tez 사용"](hdinsight-use-hive.md#usetez)을 참조하세요.

### <a name="a-nameyarnayarn"></a><a name="yarn"></a>YARN
Apache YARN은 차세대 MapReduce(MapReduce 2.0 또는 MRv2)이며 더 큰 확장성 및 실시간 처리로 MapReduce 일괄 처리를 초과하는 데이터 처리 시나리오를 지원합니다. YARN은 리소스 관리 및 분산된 응용 프로그램 프레임워크를 제공합니다. MapReduce 작업은 YARN에서 실행됩니다.

YARN에 대한 자세한 내용은 <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop NextGen MapReduce(YARN)</a>를 참조하세요.

### <a name="a-namezookeeperazookeeper"></a><a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a>는 데이터 레지스터의 공유 계층 구조 네임스페이스(znode)를 통해 대규모 분산 시스템의 프로세스를 조정합니다. Znode에는 상태, 위치, 구성 등 프로세스를 조정하기 위해 필요한 소량의 메타 정보가 들어 있습니다.

## <a name="programming-languages-on-hdinsight"></a>HDInsight의 프로그래밍 언어
HDInsight 클러스터--Hadoop, HBase, Storm 및 Spark 클러스터는 다양한 프로그래밍 언어를 지원하지만 일부는 기본적으로 설치되지 않습니다. 라이브러리의 경우 모듈 또는 패키지는 기본적으로 설치되지 않으며 스크립트 작업을 사용하여 구성 요소를 설치합니다. [HDInsight를 사용하여 스크립트 작업 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.

### <a name="default-programming-language-support"></a>기본 프로그래밍 언어 지원
기본적으로 HDInsight 클러스터는 다음을 지원합니다.

* Java
* Python

[HDInsight를 사용하여 스크립트 작업 개발](hdinsight-hadoop-script-actions-linux.md) 스크립트 작업을 사용하여 추가 언어를 설치할 수 있습니다.

### <a name="java-virtual-machine-jvm-languages"></a>Java 가상 컴퓨터(JVM) 언어
JVM(Java virtual machine)을 사용하여 Java 이외의 여러 언어를 실행할 수 있지만 이러한 언어 중 일부를 실행하려면 클러스터에 설치된 추가 구성 요소가 필요할 수 있습니다.

이러한 JVM 기반 언어는 HDInsight 클러스터에서 지원됩니다.

* Clojure
* Jython(Java용 Python)
* Scala

### <a name="hadoopspecific-languages"></a>Hadoop 관련 언어
HDInsight 클러스터는 Hadoop 에코시스템에만 적용되는 다음 언어를 지원합니다.

* Pig 작업에 대한 Pig Latin
* Hive 작업에 대한 HiveQL 및 SparkSQL

## <a name="a-nameadvantageaadvantages-of-hadoop-in-the-cloud"></a><a name="advantage"></a>클라우드에서 Hadoop이 제공하는 이점
HDInsight의 Hadoop은 Azure 클라우드 에코시스템의 일부분으로 다음과 같은 여러 가지 이점을 제공합니다.

* Hadoop 클러스터 자동 프로비저닝 수동으로 Hadoop 클러스터를 구성하는 것보다 HDInsight 클러스터를 만들기가 훨씬 쉽습니다. 자세한 내용은 [HDInsight에서 Hadoop 클러스터 프로비전](hdinsight-hadoop-provision-linux-clusters.md)을 참조하세요.
* 최신 Hadoop 구성 요소. 자세한 내용은 [HDInsight의 Hadoop 구성 요소, 버전 관리 및 서비스 제품][component-versioning]을 참조하세요.
* 클러스터의 고가용성 및 안정성. 자세한 내용은 [HDInsight에서 Hadoop 클러스터의 가용성 및 안정성](hdinsight-high-availability-linux.md) 을 참조하세요.
* Hadoop 호환 옵션인 Azure Blob 저장소를 통한 효율적이고 경제적인 데이터 저장. 자세한 내용은 [HDInsight에서 Hadoop과 Azure Blob 저장소 사용](hdinsight-hadoop-use-blob-storage.md) 을 참조하세요.
* [웹앱](https://azure.microsoft.com/documentation/services/app-service/web/) 및 [SQL Database](https://azure.microsoft.com/documentation/services/sql-database/)를 포함한 다른 Azure 서비스와의 통합.
* HDInsight 클러스터를 실행하는 추가 VM 크기와 형식. 자세한 내용은 [HDInsight의 Hadoop 구성 요소, 버전 관리 및 서비스 제품][component-versioning]을 참조하세요.
* 클러스터 크기 조정. 클러스터 크기 조정을 사용하면 HDInsight 클러스터를 삭제하거나 다시 작성하지 않고 실행 중인 HDInsight 클러스터의 노드 수를 변경할 수 있습니다.
* 가상 네트워크 지원. HDInsight를 Azure 가상 네트워크와 함께 사용하여 데이터 센터의 리소스와 클라우드 리소스를 연결하는 하이브리드 시나리오 또는 클라우드 리소스 격리를 지원할 수 있습니다.
* 저렴한 초기 비용. [무료 평가판](https://azure.microsoft.com/free/)으로 시작하거나 [HDInsight 가격 책정 정보](https://azure.microsoft.com/pricing/details/hdinsight/)를 확인해 보세요.

HDInsight의 Hadoop이 제공하는 이점에 대한 자세한 내용은 [HDInsight의 Azure 기능 페이지t][marketing-page]를 참조하세요.

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard 및 HDInsight Premium
HDInsight는 빅 데이터 클라우드 제품을 표준 및 프리미엄이라는 두 범주로 제공합니다. HDInsight 표준은 조직에서 해당 빅 데이터 워크로드를 실행하는 데 사용할 수 있는 엔터프라이즈 규모 클러스터를 제공합니다. HDInsight 프리미엄은 여기에 기반하여 HDInsight 클러스터에 대한 고급 분석 및 보안 기능을 제공합니다. 자세한 내용은 [Azure HDInsight 프리미엄](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)

## <a name="a-idresourcesaresources-for-learning-more-about-bigdata-analysis-hadoop-and-hdinsight"></a><a id="resources"></a>빅 데이터 분석, Hadoop 및 HDInsight에 대해 자세히 알아볼 수 있는 리소스
아래 리소스를 사용하여 클라우드의 Hadoop과 빅 데이터 분석에 대한 이 소개를 작성합니다.

### <a name="hadoop-documentation-for-hdinsight"></a>HDInsight용 Hadoop 설명서
* [HDInsight 설명서](https://azure.microsoft.com/documentation/services/hdinsight/): 문서, 비디오 및 추가 리소스에 대한 링크가 있는 Azure HDInsight의 Hadoop용 설명서 페이지입니다.
* [HDInsight에서 Hadoop 시작](hdinsight-hadoop-linux-tutorial-get-started.md): HDInsight Hadoop 클러스터를 프로비전하고 샘플 Hive 쿼리를 실행하는 방법에 대한 빠른 시작 자습서입니다.
* [HDInsight에서 Spark 시작](hdinsight-apache-spark-jupyter-spark-sql.md): Spark 클러스터를 만들고 대화형 Spark SQL 쿼리를 실행하는 방법에 대한 빠른 시작 자습서입니다.
* [HDInsight에서 R Server 사용](hdinsight-hadoop-r-server-get-started.md): HDInsight Premium에서 R Server를 사용하기 시작합니다.
* [HDInsight 클러스터 프로비전](hdinsight-hadoop-provision-linux-clusters.md): Azure Portal, Azure CLI 또는 Azure PowerShell을 통해 HDInsight Hadoop 클러스터를 프로비전하는 방법에 대해 알아봅니다.

### <a name="apache-hadoop"></a>Apache Hadoop
* <a target="_blank" href="http://hadoop.apache.org/">Apache Hadoop</a>: 전체 컴퓨터의 클러스터에 대해 큰 데이터 집합을 분산 처리할 수 있는 프레임워크인 Apache Hadoop 소프트웨어 라이브러리에 대해 자세히 알아 봅니다.
* <a target="_blank" href="http://hadoop.apache.org/docs/r1.0.4/hdfs_design.html">HDFS</a>: Hadoop 응용 프로그램이 사용하는 주 저장 시스템인 Hadoop 분산 파일 시스템의 아키텍처 및 설계에 대해 자세히 알아 봅니다.
* <a target="_blank" href="http://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html">MapReduce 자습서</a>: 컴퓨터 노드의 대형 클러스터에서 엄청난 양의 데이터를 병렬로 빠르게 처리하는 Hadoop 응용 프로그램을 작성하기 위한 프로그래밍 프레임워크에 대해 자세히 알아봅니다.

### <a name="microsoft-business-intelligence"></a>Microsoft 비즈니스 인텔리전스
익숙한 BI(비즈니스 인텔리전스) 도구(예: Excel, PowerPivot, SQL Server Analysis Services 및 SQL Server Reporting Services)는 파워 쿼리 추가 기능이나 Microsoft Hive ODBC 드라이버를 사용하여 HDInsight와 통합된 데이터를 가져오고 분석하고 보고합니다.

이러한 BI 도구를 통해 빅 데이터를 보다 쉽게 분석할 수 있습니다.

* [파워 쿼리로 Hadoop에 Excel 연결](hdinsight-connect-excel-power-query.md): HDInsight 클러스터와 연결된 데이터를 저장하는 Azure 저장소 계정에 Microsoft Excel용 파워 쿼리를 사용하여 Excel을 연결하는 방법을 알아 봅니다. Windows 워크스테이션이 필요합니다. Windows 또는 Linux 기반 클러스터와 함께 작동합니다.
* [Microsoft Hive ODBC 드라이버로 Hadoop에 Excel 연결](hdinsight-connect-excel-hive-odbc-driver.md): Microsoft Hive ODBC 드라이버를 사용하여 HDInsight에서 데이터를 가져오는 방법에 대해 알아봅니다. Windows 워크스테이션이 필요합니다. Windows 또는 Linux 기반 클러스터와 함께 작동합니다.
* [Microsoft 클라우드 플랫폼](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): Office 365용 Power BI에 대해 알아보고 SQL Server 평가판을 다운로드하고 SharePoint Server 2013 및 SQL Server BI를 설치합니다.
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx)
* [SQL Server Reporting Services](http://msdn.microsoft.com/library/ms159106.aspx)

[marketing-page]: https://azure.microsoft.com/services/hdinsight/
[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/



<!--HONumber=Nov16_HO2-->


