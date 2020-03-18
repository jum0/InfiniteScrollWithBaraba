# InfiniteScrollWithBaraba
This is infinite scroll example with the open source Baraba.

## 구현 화면

[참조](https://github.com/nsoojin/baraba)

## 주요 기능

- 카메라가 사용자의 얼굴을 인식하면 자동 스크롤

## 사용한 라이브러리

- [Baraba](https://github.com/nsoojin/baraba)

## 배운점

###  Simply open the Baraba.xcodeproj and run the Example scheme

Baraba `READ.md` 페이지의 `Example` 탭에 적혀있는 문장이다. 프로젝트 파일을 여는 것은 문제없었지만, 아무리 `run`을 해도 `Example` scheme이 실행되지 않았다. 문장 그대로 열고 실행하면 된다고 했지만, 이 파일 쓰라는 건가 싶어서 만든 게 이 튜토리얼이다. 아마 한 번에 알았다면 만들지 않았을까 싶다.

실행되는 것도 모른 채 수진님과 pull request를 통해 대화를 주고받으며, 실행시키려고 찾아보다가 깨달았다. 부끄러웠다.

`Scheme`의 뜻부터 찾아보니, `빌드 하려는 타깃의 집합, 빌드 할 때 사용하려는 환경 설정, 그리고 실행할 테스트의 집합`이라고 한다.

> [Documentation Archive: Xcode Scheme](https://developer.apple.com/library/archive/featuredarticles/XcodeConcepts/Concept-Schemes.html)

#### Scheme 변경하기

<img src="/Users/junmohan/Desktop/InfiniteScrollWithBaraba/Img/1.png" alt="1" style="zoom:30%;" /> <img src="/Users/junmohan/Desktop/InfiniteScrollWithBaraba/Img/2.png" alt="1" style="zoom:30%;" />

클릭 클릭

----

### use_frameworks!

`Podfile`에 있는 이 코드 한 줄을 없애지 않아, 계속 빌드가 안됐다. 하지만 해냈다. `use_framework!` 주석 처리하니 빌드가 됐다.

Cocoapod의 `use_frameworks!`는 `binary type`으로 있으면 `dynamic framework`을 지원하고 없으면 `static library`를 지원한다고 한다.  

|     Podfile      |      Support      |
| :--------------: | :---------------: |
| use_framework! ⭕️ | Dynamic framework |
| use_framework! ❌ |  Static library   |

#### use_framework!를 삭제해야 하는 이유

`use_framework!`를 사용하면 Xcode가 헤더 파일을 못 찾는다고 한다. 많은 글들을 보았지만, 이 부분에 대해서 명쾌하게 알려주는 것을 아직 찾지 못했다ㅠ

#### Library와 Framwork

- 코드를 능동적으로 사용하냐, 코드가 수동적으로 사용되냐의 차이

- ##### Library

  - 원하는 것을 만들어낼 수만 있으면 된다.
  - 라이브러니는 톱, 망치, 삽 같은 연장을 예로 들 수 있다. 사람이 들고 썰고, 바꿔들고 내려치고, 다시 바꿔들어 땅을 판다. 하지만 사람이 연장을 선택하는 입장이므로 급하면 삽으로 내려칠 수도 있고, 톱으로 땅을 긁어낼 수도 있다.

- ##### Framework

  - 이미 규칙이 정해져 있다
  - 프레임워크는 차, 비행기, 배를 예로 들 수 있다. 탈것은 정해진 곳으로만 다녀야 한다. 차를 타고 하늘을 날 수도, 배를 타고 땅으로 갈 수는 없다. 하지만, 사람이 타서 엔진을 켜고, 핸들을 돌리며, 운전하거나 조종을 한다.

#### Library vs Framework

- ##### Library

  - 라이브러리는 프로그램이 연결할 수 있는 객체 파일의 패키지 모음.
  - 라이브러리의 종류 `Static Library`와 `Shared Library` 두 가지.
    - `Static Library` - 주요 실행 파일의 코드로 패키징 된 것.
    - `Shard Library` - 실행 파일 및 추가적인 공유 객체와 공유되는 파일. Linker는 라이브러리에 대한 참조만 저장하고 라이브러리 자체는 기본 실행 파일에 패키징 되지 않음.
      - `Linker` - 컴파일러가 만들어낸 하나 이상의 목적 파일(컴파일러나 어셈블러가 소스 코드 파일을 컴파일 또는 어셈블해서 생성하는 파일)을 가져와 이를 단일 실행 프로그램으로 병합하는 프로그램.

- ##### Framework 

  - 라이브러니는 실행 파일의 코드만 있지만, 프레임워크는 공유 라이브러리와 헤더 및 기타 리소스의 하위 디렉토리를 포함하는 번들(디렉토리 구조).
    - `Bundle` - 하위 디렉토리 안에 있는 파일 디렉토리. iOS에서 번들은 이미지, nibs 또는 컴파일된 코드와 같이 하나의 패키지에 관련된 파일을 편리하게 옮기는 역할을 함. 시스템은 이것을 하나의 파일로 처리하여 내부의 구조를 알지 못해도 번들 리소스에 접근할 수 있도록 도와줌.
  - 프레임워크의 종류 `Static Framework`와 `Dynamic Framework` 두 가지.
    - `Static Framework` - Cocoa Touch Static Library에 리소스 파일을 포함한 방식.
    - `Dynamic Framework` - 앱이 실행 할 때 특정 설정 파일 기반으로 읽어 들여 실행이 되는 구조로, 앱과 달리 별도로 Framework만 업데이트하면 모두 반영이 가능.

> [Library, Framework 예시](https://kldp.org/node/124237)
>
> [Library vs Framework](http://www.knowstack.com/framework-vs-library-cocoa-ios/)
>
> [위키백과 - Linker](https://ko.wikipedia.org/wiki/링커_(컴퓨팅))
>
> [위키백과 - 목적 파일](https://ko.wikipedia.org/wiki/목적_파일)

----

### Git commit 합치기

`git rebase -i HEAD~?`를 이용한다. 물음표는 마지막 커밋을 포함하여  몇 개 불러올지.

`commit`을 세 개 했고, 메세지를 차례로 `1`, `2`, `3` 이라고 했을 때 (마지막 커밋 메세지는 `3`) 위의 명령어를 입력하면, 다음과 같은 창이 뜬다.

```
pick 4f495bf 1
pick 261df1b 2
pick a01a921 3

# Rebase 632359c..a01a921 onto 632359c (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

순서가 역으로 뜨니, 확인해야 한다. 커밋 메세지 `2`로 합치고 싶다고 하더라도, 가장 위에 있는 `pick`을 `r`로 변경하고 나머지 아래의 두 `pick`을 `s`로 변경한다.

> [참조](https://stackoverflow.com/questions/39595034/git-cannot-squash-without-a-previous-commit-error-while-rebase)

그리고 `:wq` 을 누르면 `r`로 표시했던, 1번 커밋의 메시지를 변경하라는 창이 나온다.

변경하면, 1번 커밋의 메시지가 변경되고 합쳐진 커밋들의 메시지가 나오는데, 다 지우고 최종 저장하려는 커밋 메시지를 작성 후, `:wq`를 누르면 된다.

```
# This is a combination of 3 commits.
# This is the 1st commit message:

2                                   //           최종 저장할 메세지로 변경
                                    
# This is the 2nd commit message:   //
                                    //
2                                   //
                                    //           삭제
# This is the 3rd commit message:   //
                                    //
3                                   //
                                    //
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Wed Mar 18 19:30:51 2020 +0900
#
# interactive rebase in progress; onto 632359c
# Last commands done (3 commands done):
#    squash 261df1b 2
#    squash a01a921 3
# No commands remaining.
# You are currently rebasing branch 'master' on '632359c'.
#
# Changes to be committed:
#       modified:   README.md
#

```

`git push origin +master` 명령어를 이용한다.

`commit`들이 합쳐졌으므로 `+`로 강제하고, `master`는 `branch` 이름이다.