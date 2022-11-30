# spring_cicd
github action 및 docker 를 이용한 자동 배포 시스템



<h3>github_action</h3>

1. github action

GitHub Actions는 코드 저장소(repository)로 유명한 GitHub에서 제공하는 CI(Continuous Integration, 지속 통합)와 CD(Continuous Deployment, 지속 배포)를 위한 비교적 최근에 추가된 서비스입니다. 당연히 GitHub에서 코드를 관리하고 있는 소프트웨어 프로젝트에서 사용할 수 있으며 개인은 누구나 GitHub에서 코드 저장소를 무료로 만들 수 있기 때문에 다른 CI/CD 서비스 대비 진입장벽이 낮은 편입니다.

GitHub Actions를 사용하면 자동으로 코드 저장소에서 어떤 이벤트(event)가 발생했을 때 특정 작업이 일어나게 하거나 주기적으로 어떤 작업들을 반복해서 실행시킬 수도 있습니다. 예를 들어, 누군가가 코드 저장소에 Pull Request를 생성하게 되면 GitHub Actions를 통해 해당 코드 변경분에 문제가 없는지 각종 검사를 진행할 수 있고요. 어떤 새로운 코드가 메인(main) 브랜치에 유입(push)되면 GitHub Actions를 통해 소프트웨어를 빌드(build)하고 상용 서버에 배포(deploy)할 수도 있습니다. 뿐만 아니라 매일 밤 특정 시각에 그날 하루에 대한 통계 데이터를 수집시킬 수도 있습니다.

이렇게 소프트웨어 프로젝트에서 지속적으로 수행해야하는 반복 작업들을 업계에서는 소위 CI/CD라고 많이 줄여서 부르는데요. 사람이 매번 직접 하기에는 비효율적인데다가 실수할 위험도 있기 때문에 GitHub Actions와 같은 자동화시키는 것이 유리합니다.

GitHub Actions는 기존 CI/CD 서비스 대비 간편한 설정과 높은 접근성으로 특히 개발자들 사이에서 많은 호응을 얻고 있는데요. 예전에는 CI/CD가 DevOps 엔지니어의 전유물로만 여겨지곤 했었는데 최근에는 GitHub Actions을 통해서 일반 개발자들도 어렵지 않게 CI/CD 설정을 스스로 하는 것을 보게 됩니다.

자, 그럼 지금부터 GitHub Actions를 사용하기 전에 숙지하고 있으면 큰 도움이 되는 몇 가지 핵심 개념을 살펴보도록 하겠습니다.


1. Workflows

GitHub Actions에서 가장 상위 개념인 워크플로우(Workflow, 작업 흐름)는 쉽게 말해 자동화해놓은 작업 과정이라고 볼 수 있습니다. 워크플로우는 코드 저장소 내에서 .github/workflows 폴더 아래에 위치한 YAML 파일로 설정하며, 하나의 코드 저장소에는 여러 개의 워크플로우, 즉 여러 개의 YAML 파일을 생성할 수 있습니다.

이 워크플로우 YAML 파일에는 크게 2가지를 정의해야하는데요. 첫번째는 on 속성을 통해서 해당 워크플로우가 언제 실행되는지를 정의합니다.

예를 들어, 코드 저장소의 main 브랜치에 push 이벤트가 발생할 때 마다 워크플로우를 실행하려면 다음과 같이 설정해줍니다.

.github/workflows/example.yml
on:
  push:
    branches:
      - main

jobs:
  # ...(생략)...
  
  
다른 예로, 매일 자정에 워크플로우를 실행하려면 다음과 같이 설정합니다.

.github/workflows/hello
on:
  schedule:
  - cron: "0 0 * * *"

jobs:
  # ...(생략)...
두번째는 jobs 속성을 통해서 해당 워크플로우가 구체적으로 어떤 일을 해야하는지 명시해야하는데요. 이 부분은 내용이 많으니 다음 섹션에서 알아볼까요?


  
