---

copyright:
  years: 2016, 2018
lastupdated: "2018-08-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:table: .aria-labeledby="caption"}

<!-- Name your file `at-events.md` and include it in the Reference nav group in your toc file. -->

# {{site.data.keyword.cloudaccesstrailshort}} 이벤트(엔터프라이즈 플랜)
{: #at_events}

{{site.data.keyword.Bluemix}}의 엔터프라이즈 플랜에서 사용자 및 애플리케이션이 {{site.data.keyword.messagehub}} 서비스와 어떻게 상호작용하는지 추적하려면 {{site.data.keyword.cloudaccesstrailfull}} 서비스를 사용하십시오. 
{: shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 서비스는 {{site.data.keyword.Bluemix_notm}} 내 서비스의 상태를 변경하는, 사용자가 시작한 활동을 기록합니다. 자세한 정보는 [{{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla)을 참조하십시오.

<!-- You can create different sections to group events by area. -->

## 이벤트 목록
{: #events}

<!-- Make sure you introduce the table with a detailed description that immediately precedes it. For example, see https://console.bluemix.net/docs/services/cloud-activity-tracker/services/at_events_cf.html#catalog. -->

엔터프라이즈 플랜의 {{site.data.keyword.messagehub}}는 서비스의 활동을 추적할 수 있도록 이벤트를 자동으로 생성합니다.

| 조치 |설명 |
|:-------|:------------|
| messagehub.topic.create | 토픽을 작성할 때 이벤트가 작성됨|
| messagehub.topic.delete | 토픽을 삭제할 때 이벤트가 작성됨|
{: caption="표 1. {{site.data.keyword.messagehub}} 이벤트" caption-side="top"}

## 이벤트를 볼 위치
{: #ui}

<!-- For example, choose one of the following two options. -->

<!-- Option 2: Add the following sentence if your service sends events to the account domain. -->

{{site.data.keyword.cloudaccesstrailshort}} 이벤트는 이벤트가 생성되는 {{site.data.keyword.Bluemix_notm}} 위치(지역)에서 사용 가능한 {{site.data.keyword.cloudaccesstrailshort}} **계정 도메인**에 있습니다.










