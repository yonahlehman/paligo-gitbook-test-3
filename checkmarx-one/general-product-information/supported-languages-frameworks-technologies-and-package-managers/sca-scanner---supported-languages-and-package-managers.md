# SCA Scanner - Supported Languages and Package Managers

All languages and package managers that are supported for the SCA standalone platform are also supported when running the SCA scanner in Checkmarx One.

{% hint style="info" %}
To understand how supported languages and package managers effect the scan process, see [SCA Scanner](../../scanners/sca-scanner/README.md).
{% endhint %}

{% hint style="info" %}
If you are using Checkmarx SCA Resolver, then you need to install the relevant package managers locally. For installation info, see Installing Supported Package Managers for Resolver.
{% endhint %}

### Supported Languages and Package Managers

<details>

<summary>Java</summary>

| | | | |
|---|---|---|---|
| <img src="../../../assets/download.png" alt="" width="90"> | **JVM Languages:** Java, Kotlin, Android, Groovy, Scala<br>**Additional Frameworks:** Struts, Spring<br>**Repository:** Maven Central, Sonatype, Apache<br>**File Types:** .jar<br>**Supported Languages for Exploitable Path:** Java | | |
| **Package Managers** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** |
| Maven | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `pom.xml` |
| Gradle | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/MicrosoftTeams-image__1_.png" alt="" data-size="line"> | `build.gradle` , `build.gradle.kts` |
| Ivy | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/MicrosoftTeams-image__1_.png" alt="" data-size="line"> | `ivy.xml`,<br>`build.xml` |
| SBT | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/MicrosoftTeams-image__1_.png" alt="" data-size="line"> | `build.sbt` |

</details>

<details>

<summary>JavaScript/TypeScript</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/javascript_1024x1024.png) | **Languages/Frameworks:** JavaScript, TypeScript, NodeJS, React, Angular, Apex<br>{% hint style="success" %}<br>Apex is only supported when running the scan using Checkmarx SCA Resolver with the `--extract-archives resource` argument, see Checkmarx SCA Resolver Configuration Arguments.<br>{% endhint %}<br>**Repository:** NPM<br>**File Types:** .js<br>**Supported Languages for Exploitable Path:** JavaScript | | |
| **Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with <img src="../../../assets/_blue_star_.png" alt="" data-size="line"> are required) |
| NPM | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `package.json`<img src="../../../assets/_blue_star_.png" alt="" data-size="line"> , `package-lock.json`<sup>1\]</sup> |
| Yarn (and Yarn 2) | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `package.json`<img src="../../../assets/_blue_star_.png" alt="" data-size="line"> , `yarn.lock`<img src="../../../assets/_blue_star_.png" alt="" data-size="line"><sup>1\]</sup> |
| Bower | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `bower.json` |
| Pnpm | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `pnpm-lock.yaml` |

1\] When a `lock` file is present in the project, SCA may use it to resolve dependencies. Therefore, it is important to keep the lock file up-to-date with any changes that you make in the manifest file.

</details>

<details>

<summary>.NET</summary>

| | | | |
|---|---|---|---|
| <img src="../../../assets/download.jpg" alt="" width="80"> | **Languages/Frameworks:** C#, F#, .NET, .NET Core, WCF, WPF, ASP.NET<br>**Repository:** NuGet<br>**File Types:** .dll<br>**Supported Languages for Exploitable Path:** C# | | |
| **Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** |
| NuGet | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `*.csproj` , `packages.config`, `project.assets.json`, `packages.lock.json` |

</details>

<details>

<summary>Python</summary>

| | | | |
|---|---|---|---|
| <img src="../../../assets/6414073972.png" alt="" width="80"> | **Languages/Frameworks:** Python, Django, Flask<br>**Repository:** PyPi<br>**File Types:** .egg, .whl<br>**Supported Languages for Exploitable Path:** Python | | |
| **Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with <img src="../../../assets/_blue_star_.png" alt="" data-size="line"> are required) |
| PIP | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `requirements.txt`, `requirements-*.txt`, `requirement.txt`, `requirement-*.txt` |
| Poetry | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `pyproject.toml`<img src="../../../assets/_blue_star_.png" alt="" data-size="line">, `poetry.lock` |
| Setuptools<sup> 1\]</sup> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `Setup.cfg`, `Setup.py` |
| UV | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `uv.lock`, `requirements.txt`, `pyproject.toml` |

1\] Setuptools is supported only when running scans using SCA Resolver.

</details>

<details>

<summary>PHP</summary>

| | | | |
|---|---|---|---|
| <img src="../../../assets/6412632402.png" alt="" width="80"> | **Languages/Frameworks:** PHP, Drupal<br>**Repository:** Packagist<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with <img src="../../../assets/_blue_star_.png" alt="" data-size="line"> are required) |
| Composer | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `composer.json`<img src="../../../assets/_blue_star_.png" alt="" data-size="line"> , `composer.lock` |

</details>

<details>

<summary>iOS</summary>

| | | | |
|---|---|---|---|
| <img src="../../../assets/6413779054.png" alt="" width="80"> | **Languages/Frameworks:** Swift, Objective c<br>**Repository:** GitHub<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with <img src="../../../assets/_blue_star_.png" alt="" data-size="line"> are required) |
| SwiftPm | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `Package.swift`, `Package.resolved` |
| CocoaPods | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/MicrosoftTeams-image__1_.png" alt="" data-size="line"> | `Podfile`<img src="../../../assets/_blue_star_.png" alt="" data-size="line">, `Podfile.lock` |
| Carthage | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/MicrosoftTeams-image__1_.png" alt="" data-size="line"> | `Cartfile`<img src="../../../assets/_blue_star_.png" alt="" data-size="line">, `Cartfile.private`, `Cartfile.resolved`<br>{% hint style="success" %}<br>At least one `.private` or `.resolved` file must be included.<br>{% endhint %} |

</details>

<details>

<summary>Go</summary>

| | | | |
|---|---|---|---|
| <img src="../../../assets/6413877449.png" alt="" width="80"> | **Languages/Frameworks:** Go<br>**Repository:** Golang<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with <img src="../../../assets/_blue_star_.png" alt="" data-size="line"> are required) |
| GoModules | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `go.mod`<img src="../../../assets/_blue_star_.png" alt="" data-size="line">, `go.sum` |

</details>

<details>

<summary>Ruby</summary>

| | | | |
|---|---|---|---|
| <img src="../../../assets/ruby.png" alt="" width="70"> | **Languages/Frameworks:** Ruby<br>**Repository:** RubyGems<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with <img src="../../../assets/_blue_star_.png" alt="" data-size="line"> are required) |
| RubyGems | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `Gemfile`<img src="../../../assets/_blue_star_.png" alt="" data-size="line">, `Gemfile.lock` |
| Bundler | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/MicrosoftTeams-image__1_.png" alt="" data-size="line"> | |

</details>

<details>

<summary>C++</summary>

| | | | |
|---|---|---|---|
| <img src="../../../assets/download__1_.png" alt="" width="90"> | **Languages/Frameworks:** C, C++<br>**Repository:** Conan<br>**File Types:** .cpp, .c, .h, .hpp, .a, .o, .so<br>**Exploitable Path:** Not supported<br>{% hint style="success" %}<br>C++ is supported only for File Analysis (fingerprints), not for package resolution.<br>{% endhint %} | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** |
| none | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/MicrosoftTeams-image__1_.png" alt="" data-size="line"> | none |

</details>

<details>

<summary>Unity</summary>

| | | | |
|---|---|---|---|
| <img src="../../../assets/Unity_logo_PNG10.png" alt="" width="140"> | **Languages/Frameworks:** Unity<br>**Repository:**[Unity Technologies](https://github.com/orgs/Unity-Technologies/repositories), [Needle-mirror](https://github.com/orgs/needle-mirror/repositories), [Open UPM](https://openupm.com/packages/)<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with <img src="../../../assets/_blue_star_.png" alt="" data-size="line"> are required) |
| none | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/MicrosoftTeams-image__1_.png" alt="" data-size="line"> | `manifest.json`<img src="../../../assets/_blue_star_.png" alt="" data-size="line">, `packages.json`<img src="../../../assets/_blue_star_.png" alt="" data-size="line"> |

</details>

<details>

<summary>Perl</summary>

| | | | |
|---|---|---|---|
| <img src="../../../assets/Perl_Programming_Language.png" alt="" width="100"> | **Languages/Frameworks:** Perl<br>**Repository:** [Cpan](https://www.cpan.org/)<br>**File Types:** .pl, .pm<br>**Exploitable Path:** Not supported | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** |
| Cpan | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | <img src="../../../assets/MicrosoftTeams-image__1_.png" alt="" data-size="line"> | `cpanfile`, `spcanfile.snapshot` |

</details>

<details>

<summary>Dart</summary>

| | | | |
|---|---|---|---|
| <img src="../../../assets/Picture1.jpg" alt="" width="100"> | **Languages/Frameworks:** Dart, Flutter<br>**Repository:** N/A<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** |
| Pub | <img src="../../../assets/MicrosoftTeams-image__1_.png" alt="" data-size="line"><sup>1\]</sup> | <img src="../../../assets/Check_New.png" alt="" data-size="line"> | `pubspec.lock` |

1\] Support of Pub is only for identifying malicious packages. Non-malicious packages are not shown at all in the Packages or Risks tabs.

</details>
