github 페이지 기능 사용 및 gh-pages 브랜치 작성 방법
================================================================================

github 페이지 기능 사용 방법
--------------------------------------------------------------------------------

번역 결과로 나온 html 파일은 github 페이지 기능을 사용하여 https://veranostech.github.io 로 
시작하는 웹사이트에서 바로 볼 수 있다.
github 페이지 기능을 사용 하려면 다음과 같이 설정한다.

* git 레포지토리에 에 ``gh-pages`` 라는 이름의 브랜치가 있어야 한다. 
  이 브랜치에는 페이지에 렌더링할 html 파일이 있어야 한다.

* 레포지토리의 루트 디렉토리에 ``.nojekyll`` 이라는 이름의 빈 파일이 있어야 한다.

* ``.gitignore`` 설정에 의해 무시된 파일은 렌더링되지 않으므로 build, static 등 렌더링할 파일을
  무시하고 있는 경우에는 무시 패턴을 없앤다.

* html 파일은 `https://veranostech.github.io/레포지토리이름/` 아래에 렌더링된다.

* push 하고 렌더링되려면 github 캐시 서버가 갱신되어야 하므로 몇 분 정도가 소요된다.


gh-pages 브랜치 작성 방법
--------------------------------------------------------------------------------

gh-pages 브랜치는 다른 브랜치와 달리 docs-korean 브랜치를 스핑크스로 컴파일한 결과이므로 
다른 브랜치와 달리 가장 최근의 docs-korean 브랜치에만 의존한다. 
따라서 다른 브랜치와 다르게 다음과 같이 관리한다.

1. docs-korean 브랜치에서 파일을 수정한다. 
   gh-pages 브랜치에서는 파일을 편집하면 안된다.
   반대로 docs-korean 브랜치에는 컴파일된 html 파일이 있으면 안된다.

   .. code-block:: 

      git checkout docs-korean

2. docs-korean 브랜치를 commit 한 후 gh-pages 브랜치로 checkout 한다.

   .. code-block:: 

      git add .
      git commit -m "edit"
      git checkout gh-pages

3. gh-pages 브랜치의 내용을 최신의 docs-korean 브랜치로 rebase 한다.

   .. code-block:: 

      git rebase docs-korean

4. 스핑크스 컴파일한다.

   .. code-block:: 

      make html

5. 컴파일 결과를 commit 한다.

   .. code-block:: 

      git add .
      git commit -m "build"

6. 커밋된 내용을 강제로 리모트에 push 한다.

   .. code-block:: 

      git push --force origin gh-pages


새로 포크한 레포지토리가 원래 gh-pages 브랜치를 가지는데 github page에 보이지 않을 때
--------------------------------------------------------------------------------

다음과 같이 레포지토리의 gh-pages 브랜치를 지웠다가 다시 push

  .. code-block::
  
     git checkout gh-pages
     git push origin --delete gh-pages
     git push origin



