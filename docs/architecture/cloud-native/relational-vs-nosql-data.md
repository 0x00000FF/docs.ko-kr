---
title: 관계형 및 NoSQL 데이터 비교
description: 클라우드 네이티브 응용 프로그램의 관계형 및 NoSQL 데이터에 대 한 자세한 정보
author: robvet
ms.date: 01/22/2020
ms.openlocfilehash: 5ca40791f6c6a3d04f3a7d7d9d2dbf0f23196f8f
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76795076"
---
# <a name="relational-vs-nosql-data"></a>관계형 및 NoSQL 데이터 비교

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

관계형 및 NoSQL은 클라우드 네이티브 앱에서 일반적으로 구현 되는 두 가지 유형의 데이터베이스 시스템입니다. 서로 다른 방식으로 빌드되고, 데이터를 다른 방식으로 저장 하 고, 다른 방식으로 액세스 합니다. 이 섹션에서는 두 가지 방법에 대해 살펴보겠습니다. 이 챕터의 뒷부분에서는 *Newsql*이라는 새로운 데이터베이스 기술을 살펴보겠습니다.

*관계형 데이터베이스* 는 수십 년 동안 널리 사용할 수 있는 기술입니다. 이는 완벽 하 고 검증 되며 광범위 하 게 구현 됩니다. 경쟁 데이터베이스 제품, 도구 및 전문 지식 abound. 관계형 데이터베이스는 관련 데이터 테이블의 저장소를 제공 합니다. 이러한 테이블에는 고정 스키마가 있으며, SQL (구조적 쿼리 언어)을 사용 하 여 데이터를 관리 하 고, ACID 보장을 지원 합니다.

비 *-SQL 데이터베이스* 는 고성능의 비관계형 데이터 저장소를 참조 합니다. 이러한 사용자는 사용 편의성, 확장성, 복원 력 및 가용성 특성을 사용 합니다. NoSQL은 정규화 된 데이터 테이블을 조인 하는 대신 키-값 쌍 또는 JSON 문서에 구조화 되지 않은 데이터 또는 반 구조화 된 데이터를 저장 합니다. 아니요-SQL 데이터베이스는 일반적으로 단일 데이터베이스 파티션의 범위를 벗어난 ACID 보장을 제공 하지 않습니다. 하위 초 응답 시간이 필요한 고용량 서비스는 NoSQL 데이터 저장소를 선호 합니다.

분산 클라우드 기본 시스템에 대 한 [Nosql](https://www.geeksforgeeks.org/introduction-to-nosql/) 기술의 영향은 외 수 없습니다. 이러한 공간에서 새로운 데이터 기술의 확산에는 관계형 데이터베이스에 독점적으로 의존 하는 중단 된 솔루션이 있습니다.

NoSQL 데이터베이스에는 특정 사용 사례에 적합 한 데이터에 액세스 하 고 관리 하기 위한 여러 가지 모델이 포함 됩니다. 그림 5-9에서는 네 가지 일반적인 모델을 제공 합니다.

![NoSQL 데이터 모델](./media/types-of-nosql-datastores.png)

**그림 5-9**: nosql 데이터베이스용 데이터 모델

| Model | 특성 |
| :-------- | :-------- |
| 문서 저장소 | 데이터 및 메타 데이터는 데이터베이스 내의 JSON 기반 문서에 계층적으로 저장 됩니다. |
| 키 값 저장소 | NoSQL 데이터베이스 중 가장 간단한 데이터는 키-값 쌍의 컬렉션으로 표시 됩니다. |
| 넓은 열 저장소 | 관련 데이터는 단일 열에 중첩 키/값 쌍의 집합으로 저장 됩니다. |
| 그래프 저장소 | 데이터는 그래프 구조에 노드,에 지 및 데이터 속성으로 저장 됩니다. |

## <a name="the-cap-theorem"></a>캡 정리

이러한 데이터베이스 유형 간의 차이점을 이해 하는 방법으로, 상태를 저장 하는 분산 시스템에 적용 되는 원칙 집합인 CAP 정리을 고려 합니다. 그림 5-10에서는 CAP 정리의 세 가지 속성을 보여 줍니다.

![단면 정리](./media/cap-theorem.png)

**그림 5-10**. 캡 정리

정리 분산 데이터 시스템이 일관성, 가용성 및 파티션 허용 오차를 절충 하는 것을 제공 합니다. 그리고 모든 데이터베이스에서 다음의 *세 가지 속성만을 보장할 수* 있습니다.

- *일관성.* 모든 복제본이 업데이트 될 때까지 시스템에서 요청을 차단 해야 하는 경우에도 클러스터의 모든 노드는 최신 데이터로 응답 합니다. 현재 업데이트 중인 항목에 대해 "일관 된 시스템"을 쿼리하면 모든 복제본이 성공적으로 업데이트 될 때까지 해당 응답을 기다립니다. 그러나 최신 데이터를 받게 됩니다.

- *가용성.* 모든 노드는 응답이 가장 최근 데이터가 아닌 경우에도 즉각적인 응답을 반환 합니다. 업데이트 중인 항목에 대해 "사용 가능한 시스템"을 쿼리하면 서비스에서 제공할 수 있는 가장 좋은 답을 얻을 수 있습니다.

- *파티션 허용 오차입니다.* 복제 된 데이터 노드가 실패 하거나 다른 복제 된 데이터 노드와의 연결이 끊어지는 경우에도 시스템이 계속 작동 하도록 보장 합니다.

관계형 데이터베이스는 일반적으로 일관성 및 가용성을 제공 하지만 파티션 허용 오차는 제공 하지 않습니다. 일반적으로 단일 서버에 프로 비전 되 고 컴퓨터에 리소스를 더 추가 하 여 수직으로 확장 됩니다.

대부분의 관계형 데이터베이스 시스템은 주 데이터베이스의 복사본을 다른 보조 서버 인스턴스에 만들 수 있는 기본 제공 복제 기능을 지원 합니다. 기본 인스턴스에 대 한 쓰기 작업을 수행 하 고 각 보조 복제본에 복제 합니다. 오류가 발생 하면 주 인스턴스는 보조 데이터베이스로 장애 조치 (failover) 하 여 고가용성을 제공할 수 있습니다. 보조는 읽기 작업을 배포 하는 데 사용할 수도 있습니다. 쓰기 작업이 항상 주 복제본에 대해 수행 되는 동안 읽기 작업을 보조 복제본으로 라우트 하 여 시스템 부하를 줄일 수 있습니다.

[분할](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-introduction)를 사용 하는 등의 여러 노드에 걸쳐 데이터를 가로로 분할할 수도 있습니다. 그러나 분할는 쉽게 통신할 수 없는 여러 부분에서 데이터를 spitting 하 여 운영 오버 헤드를 크게 늘립니다. 관리 하는 데 비용이 많이 들고 시간이 오래 걸릴 수 있습니다. 성능, 테이블 조인 및 참조 무결성에 영향을 줄 수 있습니다.

데이터 복제본이 "매우 일관 된" 관계형 데이터베이스 클러스터에서 네트워크 연결을 손실 하는 경우 데이터베이스에 쓸 수 없습니다. 시스템은 다른 데이터 복제본에 변경 내용을 복제할 수 없기 때문에 쓰기 작업을 거부 합니다. 모든 데이터 복제본은 트랜잭션을 완료 하기 전에 업데이트 해야 합니다.

NoSQL 데이터베이스는 일반적으로 고가용성 및 파티션 허용 오차를 지원 합니다. 보통 상용 서버에서 수평으로 확장 됩니다. 이 방법은 저렴 한 비용으로 지역 내 및 지역에 걸쳐 상당한 가용성을 제공 합니다. 이러한 컴퓨터 또는 노드 간에 데이터를 분할 하 고 복제 하 여 중복성 및 내결함성을 제공 합니다. 단점은 일관성이 있습니다. 한 NoSQL 노드의 데이터 변경 내용을 다른 노드로 전파 하는 데 다소 시간이 걸릴 수 있습니다. 일반적으로 NoSQL 데이터베이스 노드는 제공 된 데이터가 오래 되어 아직 업데이트 되지 않은 경우에도 쿼리에 즉시 응답을 제공 합니다.

데이터 복제본이 "항상 사용 가능한" NoSQL 데이터베이스 클러스터에서 연결을 분실 한 경우에도 데이터베이스에 대 한 쓰기 작업을 완료할 수 있습니다. 데이터베이스 클러스터는 쓰기 작업을 허용 하 고 각 데이터 복제본을 사용할 수 있게 되 면 업데이트 합니다.

이러한 종류의 결과는 ACID 트랜잭션이 지원 되지 않는 분산 데이터 시스템의 특성인 최종 일관성 이라고 합니다. 데이터 항목 업데이트와 각 복제본 노드에 해당 업데이트를 전파 하는 데 걸리는 시간 사이에는 짧은 지연이 있습니다. 정상적인 조건에서 지연은 일반적으로 짧고 문제가 발생 하면 늘어날 수 있습니다. 예를 들어 미국에서 NoSQL 데이터베이스의 제품 항목을 업데이트 하 고 유럽의 복제본 노드에서 동일한 데이터 항목을 쿼리 하는 경우 어떻게 되나요? 클러스터가 제품 변경 내용을 사용 하 여 유럽 노드를 업데이트할 때까지 이전 제품 정보를 받게 됩니다. 쿼리 결과를 즉시 반환 하 고 모든 복제본 노드가 업데이트 될 때까지 기다리지 않고 많은 크기와 볼륨을 얻을 수 있지만 이전 데이터를 제공할 가능성이 있습니다.

높은 가용성과 대규모 확장성은 일반적으로 강력한 일관성 보다 비즈니스에 더 중요 합니다. 개발자는 Sagas, CQRS 및 비동기 메시징과 같은 기술과 패턴을 구현 하 여 최종 일관성을 수용할 수 있습니다.

> 오늘날는 CAP 정리 제약 조건을 conidering 때 주의를 기울여야 합니다. NewSQL 이라는 새로운 유형의 데이터베이스가 등장 하 여 NoSQL 시스템의 수평적 확장성과 확장 가능한 성능을 모두 지원 하도록 관계형 데이터베이스 엔진을 확장 합니다.

## <a name="considerations-for-relational-vs-nosql-systems"></a>관계형 및 NoSQL 시스템에 대 한 고려 사항

클라우드 네이티브 기반 마이크로 서비스는 특정 데이터 요구 사항에 따라 관계형, NoSQL 데이터 저장소 또는 둘 다를 구현할 수 있습니다.

|  다음의 경우 NoSQL 데이터 저장소를 고려 합니다. | 관계형 데이터베이스를 고려해 야 하는 경우는 다음과 같습니다. | 
| :-------- | :-------- |
| 대규모의 작업 부하를 필요로 하는 많은 볼륨 작업 | 작업 볼륨이 일관적 이며 중간에서 대규모으로 확장 되어야 합니다. |
| 작업에 ACID 보장이 필요 하지 않습니다. |  ACID를 보장 해야 합니다. |
| 데이터는 동적 이며 자주 변경 됩니다. | 데이터는 예측 가능 하 고 매우 구조화 됩니다. |
| 관계 없이 데이터를 표현할 수 있습니다. | 데이터는 관계형으로로 가장 잘 표현 됩니다. |  
| 빠른 쓰기 및 쓰기 안전성이 중요 하지 않음 | 쓰기 안전은 요구 사항입니다. |  
| 데이터 검색은 간단 하 고 평평한 경향이 있습니다. | 복잡 한 쿼리 및 보고서를 사용 하 여 작업|
| 데이터에는 지리적으로 분산 되어 있어야 합니다. | 사용자의 중앙 집중화 | 
| 응용 프로그램은 공용 클라우드와 같은 상용 하드웨어에 배포 됩니다. | 응용 프로그램이 대규모의 첨단 하드웨어에 배포 됩니다. | 
|||

다음 섹션에서는 클라우드 네이티브 데이터를 저장 하 고 관리 하기 위해 Azure 클라우드에서 사용할 수 있는 옵션을 살펴보겠습니다.

## <a name="database-as-a-service"></a>Database as a Service

시작 하려면 Azure 가상 머신을 프로 비전 하 고 각 서비스에 대해 선택한 데이터베이스를 설치 하면 됩니다. 환경에 대 한 모든 권한을 보유 하 고 있는 동안 클라우드 플랫폼의 여러 기본 제공 기능을은 선형화 합니다. 또한 각 서비스에 대 한 가상 컴퓨터 및 데이터베이스를 관리할 책임이 있습니다. 이 방법을 사용 하면 시간이 많이 걸리고 비용이 많이 들 수 있습니다.

대신, 클라우드 네이티브 응용 프로그램은 [DBaaS (Database as a Service)](https://www.stratoscale.com/blog/dbaas/what-is-database-as-a-service/)로 노출 되는 데이터 서비스를 선호 합니다. 클라우드 공급 업체에 의해 완벽 하 게 관리 되는 이러한 서비스는 기본 제공 보안, 확장성 및 모니터링을 제공 합니다. 서비스를 소유 하는 대신 [지원 서비스로](./definition.md#backing-services)사용 하기만 하면 됩니다. 공급자는 규모에 따라 리소스를 작동 하 고 성능 및 유지 관리를 담당 합니다.

고가용성을 위해 클라우드 가용성 영역 및 지역에서 구성할 수 있습니다. Just-in-time 용량과 종 량 제 모델을 모두 지원 합니다. Azure는 다양 한 종류의 관리 되는 데이터 서비스 옵션을 제공 하며, 각 옵션에는 특정 혜택이 있습니다.

먼저 Azure에서 제공 되는 관계형 DBaaS 서비스를 살펴보겠습니다. Microsoft의 주력 SQL Server 데이터베이스는 몇 가지 오픈 소스 옵션과 함께 사용할 수 있습니다. 그런 다음 Azure에서 NoSQL 데이터 서비스에 대해 설명 합니다.

## <a name="azure-relational-databases"></a>Azure 관계형 데이터베이스

관계형 데이터가 필요한 클라우드 기본 마이크로 서비스의 경우, Azure는 그림 5-11에 표시 된 것 처럼 4 개의 관리 되는 관계형 DBaaS (database as a service) 제품을 제공 합니다.

![Azure의 관리 되는 관계형 데이터베이스](./media/azure-managed-databases.png)

**그림 5-11**. Azure에서 사용할 수 있는 관리 되는 관계형 데이터베이스

위의 그림에서 각은 몇 가지 추가 비용 없이 주요 기능을 제공 하는 공통 DBaaS 인프라에 배치 되는 방식을 확인 합니다.

이러한 기능은 많은 수의 데이터베이스를 프로 비전 하지만 리소스를 관리 하기 위해 제한 된 리소스를 보유 하는 조직에 특히 중요 합니다.
처리 코어, 메모리 및 기본 저장소의 크기를 선택 하 여 몇 분 내에 Azure 데이터베이스를 프로 비전 할 수 있습니다. 신속 하 게 데이터베이스를 확장 하 고 가동 중지 시간 없이 리소스를 동적으로 조정할 수 있습니다.

## <a name="azure-sql-database"></a>Azure SQL 데이터베이스

Microsoft SQL Server에 대 한 전문 지식이 있는 개발 팀은 [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)을 고려해 야 합니다. 이는 Microsoft SQL Server 데이터베이스 엔진을 기반으로 하는 완전히 관리 되는 관계형 DBaaS (As a service)입니다. 서비스는 SQL Server의 온-프레미스 버전에 있는 다양 한 기능을 공유 하 고 안정적인 최신 버전의 SQL Server 데이터베이스 엔진를 실행 합니다.

클라우드 기본 마이크로 서비스 사용 시에는 다음 세 가지 배포 옵션을 사용 하 여 Azure SQL Database를 사용할 수 있습니다.

- Single Database은 Azure 클라우드의 [Azure SQL Database 서버](https://docs.microsoft.com/azure/sql-database/sql-database-servers) 에서 실행 되는 완전히 관리 되는 SQL Database를 나타냅니다. 데이터베이스는 기본 데이터베이스 서버에 대 한 구성 종속성이 없으므로 [*포함*](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases) 된 것으로 간주 됩니다.
  
- [Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) 은 온-프레미스 SQL Server와 거의 100% 호환성을 제공 하는 완전히 관리 되는 Microsoft SQL Server 데이터베이스 엔진 인스턴스입니다. 이 옵션은 최대 35 TB의 더 큰 데이터베이스를 지원 하 고 더 나은 격리를 위해 [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 에 배치 됩니다.

- [서버](https://docs.microsoft.com/azure/sql-database/sql-database-serverless) 를 사용 하지 않는 Azure SQL Database는 워크 로드 요구 사항에 따라 자동으로 크기를 조정 하는 단일 데이터베이스의 계산 계층입니다. 초당 사용 된 계산의 양에 대해서만 요금을 청구 합니다. 서비스는 일정 하지 않은 간헐적 사용 패턴과 비활성 기간을 포함 하는 워크 로드에 적합 합니다. 서버를 사용 하지 않는 계산 계층은 비활성 기간 동안에도 데이터베이스를 자동으로 일시 중지 하므로 저장소 요금만 청구 됩니다. 작업이 반환 되 면 자동으로 다시 시작 됩니다.

기존 Microsoft SQL Server stack 외에도 Azure는 세 개의 인기 있는 오픈 소스 데이터베이스의 관리 되는 버전을 제공 합니다.

## <a name="open-source-databases-in-azure"></a>Azure에서 오픈 소스 데이터베이스

오픈 소스 관계형 데이터베이스는 클라우드 네이티브 응용 프로그램에 널리 사용 됩니다. 많은 기업에서 특히 비용 절감을 위해 상업적 데이터베이스 제품을 통해이를 선호 합니다. 대부분의 개발 팀은 유연성, 커뮤니티 지원 개발 및 도구 및 확장의 에코 시스템을 이용 합니다. 오픈 소스 데이터베이스는 여러 클라우드 공급자에 배포 될 수 있으므로 "공급 업체의 잠금" 문제를 최소화 하는 데 도움이 됩니다.

개발자는 Azure VM에서 오픈 소스 데이터베이스를 쉽게 자체 호스트할 수 있습니다. 이 방법은 모든 권한을 제공 하는 동안 데이터베이스 및 VM의 관리, 모니터링 및 유지 관리를 위한 후크를 제공 합니다.

그러나 Microsoft는 널리 사용 되는 여러 오픈 소스 데이터베이스를 *완전히 관리 되* 는 dbaas 서비스로 제공 하 여 Azure를 "오픈 플랫폼"으로 유지 하는 노력을 지속적으로 제공 합니다.

### <a name="azure-database-for-mysql"></a>Azure Database for MySQL

[MySQL](https://en.wikipedia.org/wiki/MySQL) 은 오픈 소스 관계형 데이터베이스 이며 [램프 소프트웨어 스택에](https://en.wikipedia.org/wiki/LAMP_(software_bundle))빌드된 응용 프로그램에 대 한 기둥입니다. *읽기* 작업이 많은 워크 로드에 대해 널리 선택 되어 있으며, Facebook, Twitter, YouTube 등 많은 대규모 조직에서 사용 됩니다. Community edition은 무료로 제공 되지만 enterprise edition에는 라이선스 구매가 필요 합니다. 원래 1995에 생성 된 제품은 2008의 Sun Microsystems에서 구매 했습니다. Oracle에서 Sun 및 MySQL 2010을 얻었습니다.

[Azure Database for MySQL](https://azure.microsoft.com/services/mysql/) 는 오픈 소스 MySQL 서버 엔진을 기반으로 하는 관리 되는 관계형 데이터베이스 서비스입니다. MySQL Community edition을 사용 합니다. Azure MySQL 서버는 서비스에 대 한 관리 지점입니다. 이는 온-프레미스 배포에 사용 되는 것과 동일한 MySQL 서버 엔진입니다. 엔진은 서버당 단일 데이터베이스 또는 리소스를 공유 하는 서버당 여러 데이터베이스를 만들 수 있습니다. 새 기술에 대해 알아보거나 가상 머신을 관리할 필요 없이 동일한 오픈 소스 도구를 사용 하 여 데이터를 계속 관리할 수 있습니다.

### <a name="azure-database-for-mariadb"></a>Azure Database for MariaDB

[Mariadb](https://mariadb.com/) 서버는 다른 인기 있는 오픈 소스 데이터베이스 서버입니다. 이는 MySQL을 소유한 Sun Microsystems를 구매한 경우 MySQL의 *포크* 로 생성 되었습니다. 이는 MariaDB가 오픈 소스를 유지 하도록 하기 위한 것입니다. MariaDB는 MySQL의 포크 이며, 데이터 및 테이블 정의는 호환 되며 클라이언트 프로토콜, 구조 및 Api는 결합 됩니다.

MariaDB는 강력한 커뮤니티 이며 많은 대기업에서 사용 됩니다. Oracle은 계속 해 서 MySQL을 유지 관리 하 고, 개선 하 고, 지원 하며,이 경우에는 Aadb foundation이 MariaDB를 관리 하 여 제품 및 설명서에 대 한 공용 기여를 허용

[Azure Database for MariaDB](https://azure.microsoft.com/services/mariadb/) 은 Azure 클라우드에서 완전히 관리 되는 관계형 Database as a Service입니다. 이 서비스는 MariaDB community edition 서버 엔진을 기반으로 합니다. 예측 가능한 성능과 동적 확장성으로 중요 업무용 워크 로드를 처리할 수 있습니다.

### <a name="azure-database-for-postgresql"></a>Azure Database for PostgreSQL

[PostgreSQL](https://www.postgresql.org/) 는 30 년 이상 활성 개발이 포함 된 오픈 소스 관계형 데이터베이스입니다. PostgresSQL는 안정성 및 데이터 무결성에 대 한 강력한 평판을 갖습니다. 기능이 풍부 하 고 SQL에서 호환 되며, 특히 복잡 한 쿼리와 많은 쓰기 작업의 경우에는 MySQL 보다 성능이 더 우수 합니다. Apple, Red Hat 및 Fujitsu를 비롯 한 많은 대기업은 PostgreSQL를 사용 하 여 제품을 구축 했습니다.

[Azure Database for PostgreSQL](https://azure.microsoft.com/services/postgresql/) 은 오픈 소스 Postgres 데이터베이스 엔진을 기반으로 하는 완전히 관리 되는 관계형 데이터베이스 서비스입니다. 이 서비스는 Java, Python, Node C++, C\#및 PHP를 비롯 한 다양 한 개발 플랫폼을 지원 합니다. [명령줄 인터페이스](https://datamigration.microsoft.com/scenario/postgresql-to-azurepostgresql?step=1) 도구나 Azure 데이터 마이그레이션 서비스를 사용 하 여 PostgreSQL 데이터베이스를이 데이터베이스로 마이그레이션할 수 있습니다.

Azure Database for PostgreSQL는 다음과 같은 두 가지 배포 옵션을 사용할 수 있습니다. 

- [단일 서버](https://docs.microsoft.com/azure/postgresql/concepts-servers) 배포 옵션은 여러 데이터베이스를 배포할 수 있는 여러 데이터베이스에 대 한 중앙 관리 지점입니다. 가격은 코어 및 저장소에 따라 서버 별로 구성 됩니다.

- [Citus (Hyperscale) 옵션](https://azure.microsoft.com/blog/get-high-performance-scaling-for-your-azure-database-workloads-with-hyperscale/) 은 Citus Data 기술을 기반으로 합니다. 고성능 및 확장성을 제공 하기 위해 수백 개의 노드에서 단일 데이터베이스를 *수평으로 확장* 하 여 성능을 향상 시킬 수 있습니다. 이 옵션을 사용 하면 엔진은 메모리에 더 많은 데이터를 맞추고, 수백 개의 노드에서 쿼리를 병렬화 하 고, 데이터를 더 빠르게 인덱싱할 수 있습니다. 

## <a name="nosql-data-in-azure"></a>Azure의 NoSQL 데이터

Cosmos DB은 Azure 클라우드에서 완전히 관리 되는 전역으로 분산 된 NoSQL 데이터베이스 서비스입니다. 공동 Ca-콜라, Skype, ExxonMobil 및 Liberty 상호을 포함 하 여 전 세계 많은 기업 들이 채택 했습니다.

서비스에 전 세계 어디에서 든 빠른 응답이 필요한 경우에는 Cosmos DB를 선택 하는 것이 좋습니다. 그림 5-12은 Cosmos DB를 보여 줍니다.

![Cosmos DB 개요](./media/cosmos-db-overview.png)

**그림 5-12**: Cosmos DB 개요

위의 그림은 Cosmos DB에서 사용할 수 있는 여러 기본 제공 클라우드 기본 기능을 보여 줍니다. 이 섹션에서는이에 대해 좀 더 자세히 살펴보겠습니다.

### <a name="global-support"></a>글로벌 지원

클라우드 네이티브 응용 프로그램은 종종 글로벌 대상이 있고 글로벌 확장이 필요 합니다.

Cosmos 데이터베이스를 지역 또는 전 세계에 분산 하 고, 데이터를 사용자에 게 가깝게 배치 하 고, 응답 시간을 개선 하 고, 대기 시간을 줄일 수 있습니다. 서비스를 일시 중지 하거나 다시 배포 하지 않고 지역에서 데이터베이스를 추가 하거나 제거할 수 있습니다. 백그라운드에서 Cosmos DB는 구성 된 각 지역에 데이터를 투명 하 게 복제 합니다.

Cosmos DB는 전역 수준에서 [능동/능동](https://kemptechnologies.com/white-papers/unfog-confusion-active-passive-activeactive-load-balancing/) 클러스터링을 지원 하 여 *쓰기 및 읽기를 모두*지원 하도록 데이터베이스 영역을 구성할 수 있도록 합니다.

[다중 마스터](https://docs.microsoft.com/azure/cosmos-db/multi-master-benefits) 프로토콜은 다음과 같은 기능을 가능 하 게 하는 Cosmos DB의 중요 한 기능입니다.

- 무제한 탄력적 쓰기 및 읽기 확장성.

- 전 세계의 모든 읽기 및 쓰기 가용성 99.999%

- 99 번째 백분위 수에서 10 밀리초 이내에 보장 된 읽기 및 쓰기가 제공 됩니다.

Cosmos DB [멀티 호 밍 api](https://docs.microsoft.com/azure/cosmos-db/distribute-data-globally)를 사용 하면 마이크로 서비스에서 가장 가까운 Azure 지역을 자동으로 인식 하 여 요청을 보냅니다. 가장 가까운 지역은 구성 변경 없이 Cosmos DB로 식별 됩니다. 지역을 사용할 수 없게 되 면 멀티 호 밍 기능이 요청을 사용 가능한 가장 가까운 다음 지역으로 자동으로 라우팅합니다.

### <a name="multi-model-support"></a>다중 모델 지원

응용 프로그램을 클라우드 기본 아키텍처로 모놀리식 하는 경우 개발 팀은 경우에 따라 오픈 소스 NoSQL 데이터 저장소를 마이그레이션해야 합니다. Cosmos DB를 통해 이러한 NoSQL 데이터 저장소에 *대 한 투자를 다중 모델* 데이터 플랫폼과 함께 유지할 수 있습니다. 그림 5-13에서는 지원 되는 NoSQL [호환성 api](https://www.wikiwand.com/en/Cosmos_DB)를 보여 줍니다.

![Cosmos DB 공급자](./media/cosmos-db-providers.png)

**그림 5-13**: Cosmos DB 공급자

개발 팀은 데이터 나 코드를 최소한으로 변경 하 여 기존 Mongo, Gremlin 또는 Cassandra 데이터베이스를 Cosmos DB로 마이그레이션할 수 있습니다. 새 앱의 경우 개발 팀은 오픈 소스 옵션 또는 기본 제공 SQL API 모델 중에서 선택할 수 있습니다.

> 내부적으로 Cosmos는 데이터를 기본 데이터 형식으로 구성 된 간단한 구조체 형식으로 저장 합니다. 각 요청에 대해 데이터베이스 엔진은 기본 데이터를 선택한 모델 표현으로 변환 합니다.

위의 그림에서 5-13는 [Table API](https://docs.microsoft.com/azure/cosmos-db/table-introduction) 옵션을 확인 합니다. 이 API는 Azure Table Storage의 진화입니다. 둘 다 동일한 기본 테이블 모델을 공유 하지만 Cosmos DB Table API는 Azure Storage API에서 사용할 수 없는 프리미엄 향상 기능을 추가 합니다. 이러한 기능은 그림 5-4에서 대조 됩니다.

![Azure Table API](media/azure-table-api.png)

**그림 5-14**: Azure Table API 공급자

Azure 테이블 저장소를 사용 하는 마이크로 서비스는 Cosmos DB Table API 쉽게 마이그레이션할 수 있습니다. 코드를 변경할 필요가 없습니다.

### <a name="tunable-consistency"></a>튜닝 가능한 일관성

이전에는 *관계형 vs와 NoSQL* 섹션에서 *데이터 일관성*의 주제에 대해 설명 했습니다. 데이터 일관성은 데이터의 *무결성* 을 의미 합니다. 분산 데이터를 사용 하는 클라우드 네이티브 서비스는 복제를 사용 하며 읽기 일관성, 가용성 및 대기 시간 간에 기본적인 균형을 유지 해야 합니다.

대부분의 분산 데이터베이스를 통해 개발자는 두 가지 일관성 모델 (강력한 일관성과 최종 일관성) 중에서 선택할 수 있습니다. *강력한 일관성* 은 데이터 프로그래밍의 골드 표준입니다. 모든 데이터베이스 복사본에서 업데이트가 복제 될 때까지 대기 시간이 발생 해야 하는 경우에도 쿼리가 항상 최신 데이터를 반환 하도록 보장 합니다. *최종 일관성* 을 위해 구성 된 데이터베이스는 해당 데이터가 최신 복사본이 아니더라도 데이터를 즉시 반환 합니다. 후자 옵션을 사용 하면 더 높은 가용성, 더 큰 규모 및 향상 된 성능을 제공 합니다.

Azure Cosmos DB는 그림 5-15에 표시 된 잘 정의 된 5 가지 [일관성 모델](https://docs.microsoft.com/azure/cosmos-db/consistency-levels) 을 제공 합니다.

![Cosmos DB 일관성 그래프](./media/cosmos-consistency-level-graph.png)

**그림 5-15**: Cosmos DB 일관성 수준

 이러한 옵션을 사용 하면 일관성, 가용성 및 데이터에 대 한 성능을 세밀 하 게 선택 하 고 세분화 된 균형을 유지할 수 있습니다. 그림 5-16에서는 각 수준에 대해 설명 합니다.

![Cosmos DB 일관성 수준](./media/cosmos-db-consistency-levels.png)

**그림 5-16**: Cosmos DB 일관성 수준 설명

[9 계층 Cosmos DB 설명](https://blog.jeremylikness.com/blog/2018-03-23_getting-behind-the-9ball-cosmosdb-consistency-levels/)하는 문서에서 설명 Microsoft 클라우드 하는 일관성 수준에 대 한 자세한 내용은 개발자 대표 Jeremy Likeness에서 5 가지 모델에 대 한 뛰어난 설명을 제공 합니다.

### <a name="partitioning"></a>분할

자동 [분할](https://docs.microsoft.com/azure/cosmos-db/partitioning-overview) 을 채택 하 여 클라우드 네이티브 서비스의 성능 요구에 맞게 데이터베이스 크기를 조정 하는 Azure Cosmos DB.

데이터베이스, 컨테이너 및 항목을 만들어 Cosmos DB 데이터에서 데이터를 관리 합니다.

컨테이너는 Cosmos DB 데이터베이스에 있으며 스키마를 구분 하지 않는 항목 그룹을 나타냅니다. 항목은 컨테이너에 추가 하는 데이터입니다. 문서, 행, 노드 또는 가장자리로 표시 됩니다. 컨테이너에 추가 된 모든 항목은 자동으로 인덱싱됩니다.

컨테이너를 분할 하기 위해 항목은 논리적 파티션 이라는 별개의 하위 집합으로 나뉩니다. 논리적 파티션은 컨테이너의 각 항목과 연결 된 파티션 키의 값에 따라 채워집니다. 그림 5-18에는 파티션 키 값을 기반으로 하는 논리적 파티션이 있는 두 개의 컨테이너가 나와 있습니다.

![Cosmos DB 분할 메커니즘](./media/cosmos-db-partitioning.png)

**그림 5-18**: Cosmos DB 분할 메커니즘

위의 그림에서 각 항목에는 ' city ' 또는 ' 공항 '의 파티션 키가 포함 되어 있습니다. 키는 항목의 논리적 파티션을 결정 합니다. 도시 코드가 있는 항목은 왼쪽의 컨테이너에 할당 되 고, 공항 코드를 포함 하는 항목은 오른쪽의 컨테이너에 할당 됩니다. 파티션 키 값을 ID 값과 결합 하면 항목을 고유 하 게 식별 하는 항목의 인덱스가 생성 됩니다.

내부적으로 Cosmos DB는 컨테이너의 확장성 및 성능 요구를 충족 하기 위해 물리적 파티션의 [논리 파티션](https://docs.microsoft.com/azure/cosmos-db/partition-data) 배치를 자동으로 관리 합니다. 응용 프로그램 처리량 및 저장소 요구 사항이 증가 하면 더 많은 서버에서 논리적 파티션을 재배포 Azure Cosmos DB. 재배포 작업은 Cosmos DB에서 관리 되며 중단 또는 가동 중지 시간 없이 호출 됩니다.

## <a name="newsql-databases"></a>NewSQL 데이터베이스

*Newsql* 는 nosql의 분산 확장성과 관계형 데이터베이스의 ACID 보증을 결합 하는 새로운 데이터베이스 기술입니다. NewSQL 데이터베이스는 전체 트랜잭션 지원 및 ACID 규정에 따라 분산 된 환경에서 대용량 데이터를 처리 해야 하는 비즈니스 시스템에 중요 합니다. NoSQL 데이터베이스는 대규모 확장성을 제공할 수 있지만 데이터 일관성을 보장 하지는 않습니다. 일관 되지 않은 데이터의 일시적인 문제는 개발 팀에 부담을 수 있습니다. 개발자는 일관성 없는 데이터로 인해 발생 하는 문제를 관리 하기 위해 마이크로 서비스 코드로 보호를 구성 해야 합니다.

CNCF (Cloud Native 컴퓨팅 Foundation)는 여러 NewSQL 데이터베이스 프로젝트를 제공 합니다.

| 프로젝트 | 특성 |
| :-------- | :-------- |
| Cockroach DB |전체적으로 크기를 조정 하는 ACID 규격 관계형 데이터베이스입니다. 클러스터에 새 노드를 추가 하 고 CockroachDB는 인스턴스 및 지역 간에 데이터를 분산 합니다. 안정성을 보장 하기 위해 복제본을 만들고, 관리 하 고, 배포 합니다. 오픈 소스 이며 자유롭게 사용할 수 있습니다.  |
| TiDB | HTAP (하이브리드 트랜잭션 및 분석 처리) 워크 로드를 지 원하는 오픈 소스 데이터베이스입니다. 이 기능은 MySQL과 호환 되며 가로 확장성, 강력한 일관성 및 고가용성을 제공 합니다.  TiDB는 MySQL 서버 처럼 작동 합니다. 응용 프로그램에 대 한 광범위 한 코드 변경을 요구 하지 않고 기존 MySQL 클라이언트 라이브러리를 계속 사용할 수 있습니다. |
| YugabyteDB | 오픈 소스, 고성능 분산 SQL database 낮은 쿼리 대기 시간, 오류에 대 한 복원 력 및 글로벌 데이터 배포를 지원 합니다. YugabyteDB는 PostgressSQL 호환 되며 확장 RDBMS 및 인터넷 규모 OLTP 워크 로드를 처리 합니다. 이 제품은 NoSQL도 지원 하며 Cassandra와 호환 됩니다. |
|Vitess | Vitess는 MySQL 인스턴스의 규모가 많은 클러스터를 배포, 확장 및 관리 하기 위한 데이터베이스 솔루션입니다. 공용 또는 사설 클라우드 아키텍처에서 실행할 수 있습니다. 수직 및 수평 분할 지원에 대 한 여러 중요 한 MySQL 기능과 기능을 결합 하 고 확장 합니다. YouTube에서 발생 한 Vitess는 2011부터 모든 YouTube 데이터베이스 트래픽을 처리 했습니다. |

이전 그림의 오픈 소스 프로젝트는 Cloud Native 컴퓨팅 Foundation에서 사용할 수 있습니다. 이러한 제품 중 세 가지는 .NET Core 지원을 포함 하는 전체 데이터베이스 제품입니다. 다른 Vitess는 MySQL 인스턴스의 규모가 많은 클러스터를 수평으로 확장 하는 데이터베이스 클러스터링 시스템입니다. 

NewSQL 데이터베이스의 핵심 디자인 목표는 플랫폼의 복원 력 및 확장성을 활용 하 여 Kubernetes에서 기본적으로 작동 하는 것입니다.

NewSQL 데이터베이스는 기본 가상 컴퓨터를 다시 시작 하거나 잠시 후에 다시 예약할 수 있는 임시 클라우드 환경에서 올립니다 하도록 설계 되었습니다. 데이터베이스는 데이터 손실 또는 가동 중지 시간 없이 노드 오류를 계속 발생 시 키도 록 설계 되었습니다. 예를 들어 CockroachDB는 클러스터의 노드에 있는 데이터의 세 가지 일관성 있는 복제본을 유지 관리 하 여 컴퓨터 손실을 감당할 수 있습니다.

Kubernetes는 *서비스 구문을* 사용 하 여 클라이언트가 단일 DNS 항목에서 동일한 newsql database 프로세스 그룹의 주소를 지정할 수 있도록 합니다. 연결 된 서비스의 주소에서 데이터베이스 인스턴스를 분리 하면 기존 응용 프로그램 인스턴스를 방해 하지 않고 확장할 수 있습니다. 지정 된 시간에 서비스에 요청을 보내면 항상 동일한 결과가 반환 됩니다.

이 시나리오에서 모든 데이터베이스 인스턴스는 동일 합니다. 기본 또는 보조 관계가 없습니다. CockroachDB에서 발견 된 *합의 복제* 와 같은 기술은 모든 데이터베이스 노드에서 모든 요청을 처리할 수 있도록 합니다. 부하 분산 된 요청을 받는 노드에 로컬에서 필요한 데이터가 있으면 즉시 응답 합니다. 그렇지 않으면 노드가 게이트웨이가 되며 적절 한 노드에 요청을 전달 하 여 올바른 답을 가져옵니다. 클라이언트의 관점에서 보면 모든 데이터베이스 노드는 동일 합니다. 즉, 백그라운드에서 작동 하는 수십 개 또는 수백 개의 노드가 있더라도 단일 컴퓨터 시스템의 일관성을 보장 하는 단일 *논리* 데이터베이스로 표시 됩니다.

NewSQL 데이터베이스의 메커니즘에 대 한 자세한 내용은 [대시: Kubernetes 데이터베이스의 네 가지 속성](https://thenewstack.io/dash-four-properties-of-kubernetes-native-databases/) 문서를 참조 하세요.

## <a name="data-migration-to-the-cloud"></a>클라우드로 데이터 마이그레이션

시간이 많이 걸리는 작업 중 하나는 데이터 플랫폼 간에 데이터를 마이그레이션하는 것입니다. [Azure 데이터 마이그레이션 서비스](https://azure.microsoft.com/services/database-migration/) 를 통해 이러한 활동을 신속 하 게 수행할 수 있습니다. 가동 중지 시간을 최소화 하면서 여러 외부 데이터베이스 소스에서 Azure 데이터 플랫폼으로 데이터를 마이그레이션할 수 있습니다. 대상 플랫폼에는 다음과 같은 서비스가 포함 됩니다.

- Azure SQL 데이터베이스
- Azure Database for MySQL
- Azure Database for MariaDB
- Azure Database for PostgreSQL
- CosmosDB
  
서비스에서는 마이그레이션을 실행 하는 데 필요한 변경 사항 (중소 규모)을 안내 하는 권장 사항을 제공 합니다.

>[!div class="step-by-step"]
>[이전](Database-per-microservice.md)
>[다음](azure-caching.md)