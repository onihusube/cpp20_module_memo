# C++20 モジュール めも

[P1103R3 Merging Modules](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1103r3.pdf)を読んだ時に訳したメモと規格文書からモジュール関連の部分を抽出して和訳したもの。

- [P1103R3の翻訳](./p1103r3_memo.md)
- [C++20モジュール関連規格記述の翻訳](./cpp20_module_memo.md)

※読み進めながら書いてたので記法に一貫性がないです。  
※翻訳には多分に間違いが含まれています、怪しい記述を信用しないでください。

## 関連する文書等の一覧

- [P1103R3 : Merging Modules](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1103r3.pdf)
- [[module.interface] Use 'namespace-definition', #2916 - C++ Standard Draft Sources](https://github.com/cplusplus/draft/pull/2916)
- [Typo fixes for sample code comments related to modules. #2951 - C++ Standard Draft Sources](https://github.com/cplusplus/draft/pull/2951)
- [[basic.lookup.argdep]/5 Added export to `apply(T t, U u)` #2973 - C++ Standard Draft Sources](https://github.com/cplusplus/draft/pull/2973)
- [P1811R0 : Relaxing redefinition restrictions for re-exportation robustness](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1811r0.html)
- [P1766R1 : Mitigating minor modules maladies](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1766r1.html)
- [P1703R1 : Recognizing Header Unit Imports Requires Full Preprocessing](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1703r1.html)
- [P1502R1 : Standard library header units for C++20](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1502r1.html)
- [GB022 04.01Allow "import" for accessing standard library names](https://github.com/cplusplus/nbballot/issues/22)
    - [[intro.compliance] The standard library also offers header units. - C++ Standard Draft Sources](https://github.com/cplusplus/draft/pull/3356)
- [FR039 06.05.2.4 Non-exported functions should not be visible via ADL after importing](https://github.com/cplusplus/nbballot/issues/38)
    - [[basic.lookup.argdep] Inline the definition of 'interface'. - C++ Standard Draft Sources](https://github.com/cplusplus/draft/pull/3390)
- [GB 078 10.01 Harmonize "digits" referring to reserved namespace/module names](https://github.com/cplusplus/nbballot/issues/77)
    - [[namespace.future,diff.cpp14.library] Properly refer to grammar 'digit'](https://github.com/cplusplus/draft/pull/3345)
- [P1971R0 : Core Language Changes for NB Comments at the November, 2019 (Belfast) meeting](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1971r0.html)
    - [GB079 10.01 Add example for private-module-fragment](https://github.com/cplusplus/nbballot/issues/78)
    - [US087 10.03 p9 Header unit imports cannot be cyclic, either](https://github.com/cplusplus/nbballot/issues/86)
    - [US132 15.03 Macros from the command-line not exported by header units](https://github.com/cplusplus/nbballot/issues/131)
- [P1979R0 : Resolution to US086](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1979r0.html)
    - [US086 10.03 Treatment of non-exported imports](https://github.com/cplusplus/nbballot/issues/85)
- [US088 10.04 [module.global] Harmonize labels referring to the global module fragment](https://github.com/cplusplus/nbballot/issues/87)
    - [[module.global,cpp.glob.frag] Rename labels to ...global.frag.](https://github.com/cplusplus/draft/pull/3351)
- [GB089 10.06 [module.reach] Mark translation unit boundaries in example](https://github.com/cplusplus/nbballot/issues/88)
  - [[module.reach] Clearly separate translation units in example.](https://github.com/cplusplus/draft/pull/3331)
- [P1874R1 Dynamic Initialization Order of Non-Local Variables in Modules](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1874r1.html)
    - [US082 10.03 [module.import] Define order of initialization for globals in modules P1874](https://github.com/cplusplus/nbballot/issues/81)
- [P2103R0 Core Language Changes for NB Comments at the February, 2020 (Prague) meeting](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2020/p2103r0.html)
    - [NB US 033: Allow import inside linkage-specifications](https://github.com/cplusplus/nbballot/issues/32)
- [P1779R3: ABI isolation for member functions](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2020/p1779r3.html)
- [P1857R3 Modules Dependency Discovery](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2020/p1857r3.html)
- [P2109R0: US084: Disallow "export import foo" outside of module interface](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2020/p2109r0.html)
- [P1815R2: Translation-unit-local entities](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2020/p1815r2.html)

### 未追記

- [P1971R0 : Core Language Changes for NB Comments at the November, 2019 (Belfast) meeting](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1971r0.html)
    - [US367 6-15 Instead of header inclusion, also permit header unit import](https://github.com/cplusplus/nbballot/issues/363)
      - `new`とか`<=>`とか対応するヘッダのインクルードが必要なものについて、`import`を明示的に許可する。
- [P2115R0: US069: Merging of multiple definitions for unnamed unscoped enumerations](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2020/p2115r0.html)
- [P1787R6 Declarations and where to find them](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2020/p1787r6.html)
