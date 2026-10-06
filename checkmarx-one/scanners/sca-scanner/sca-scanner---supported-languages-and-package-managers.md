# SCA Scanner - Supported Languages and Package Managers

All languages and package managers that are supported for the SCA standalone platform are also supported when running the SCA scanner in Checkmarx One.

{% hint style="info" %}
To understand how supported languages and package managers effect the scan process, see [Understanding the Scan Process](README.md#understanding-the-scan-process).
{% endhint %}

{% hint style="info" %}
If you are using Checkmarx SCA Resolver, then you need to install the relevant package managers locally. For installation info, see Installing Supported Package Managers for Resolver.
{% endhint %}

### Supported Languages and Package Managers

<details>

<summary>Java</summary>

| | | | | | |
|---|---|---|---|---|---|
| ![](../../../assets/download.png) | **JVM Languages:** Java, Kotlin, Android, Groovy, Scala<br>**Additional Frameworks:** Struts, Spring<br>**Repository:** Maven Central, Sonatype, Apache<br>**File Types:** .jar<br>**Supported Languages for Exploitable Path:** Java | | | | |
| **Package Managers** | **Vulnerability Support** | **Malicious Package Support** | | **Manifest Files** | |
| Maven | | | | `pom.xml` | |
| Gradle | | | | `build.gradle` , `build.gradle.kts` | |
| Ivy | | | | `ivy.xml`,<br>`build.xml` | |
| SBT | | | | `build.sbt` | |

</details>

<details>

<summary>JavaScript/TypeScript</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/javascript_1024x1024.png) | **Languages/Frameworks:** JavaScript, TypeScript, NodeJS, React, Angular, Apex<br>{% hint style="success" %}<br>Apex is only supported when running the scan using Checkmarx SCA Resolver with the `--extract-archives resource` argument, see Checkmarx SCA Resolver Configuration Arguments.<br>{% endhint %}<br>**Repository:** NPM<br>**File Types:** .js<br>**Supported Languages for Exploitable Path:** JavaScript | | |
| **Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with ![](../../../assets/_blue_star_.png) are required) |
| NPM | | | `package.json`![](../../../assets/_blue_star_.png) , `package-lock.json`<sup>1\]</sup> |
| Yarn (and Yarn 2) | | | `package.json`![](../../../assets/_blue_star_.png) , `yarn.lock`![](../../../assets/_blue_star_.png)<sup>1\]</sup> |
| Bower | | | `bower.json` |
| Pnpm | | | `pnpm-lock.yaml` |

1\] When a `lock` file is present in the project, SCA may use it to resolve dependencies. Therefore, it is important to keep the lock file up-to-date with any changes that you make in the manifest file.

</details>

<details>

<summary>.NET</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/download.jpg) | **Languages/Frameworks:** C#, F#, .NET, .NET Core, WCF, WPF, ASP.NET<br>**Repository:** NuGet<br>**File Types:** .dll<br>**Supported Languages for Exploitable Path:** C# | | |
| **Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** |
| NuGet | | | `*.csproj` , `packages.config`, `project.assets.json`, `packages.lock.json` |

</details>

<details>

<summary>Python</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/6414073972.png) | **Languages/Frameworks:** Python, Django, Flask<br>**Repository:** PyPi<br>**File Types:** .egg, .whl<br>**Supported Languages for Exploitable Path:** Python | | |
| **Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with ![](../../../assets/_blue_star_.png) are required) |
| PIP | | | `requirements.txt`, `requirements-*.txt`, `requirement.txt`, `requirement-*.txt` |
| Poetry | | | `pyproject.toml`![](../../../assets/_blue_star_.png), `poetry.lock` |
| Setuptools<sup> 1\]</sup> | | | `Setup.cfg`, `Setup.py` |
| UV | | | `uv.lock`, `requirements.txt`, `pyproject.toml` |

1\] Setuptools is supported only when running scans using SCA Resolver.

</details>

<details>

<summary>PHP</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/6412632402.png) | **Languages/Frameworks:** PHP, Drupal<br>**Repository:** Packagist<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with ![](../../../assets/_blue_star_.png) are required) |
| Composer | | | `composer.json`![](../../../assets/_blue_star_.png) , `composer.lock` |

</details>

<details>

<summary>iOS</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/6413779054.png) | **Languages/Frameworks:** Swift, Objective c<br>**Repository:** GitHub<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with ![](../../../assets/_blue_star_.png) are required) |
| SwiftPm | | | `Package.swift`, `Package.resolved` |
| CocoaPods | | | `Podfile`![](../../../assets/_blue_star_.png), `Podfile.lock` |
| Carthage | | | `Cartfile`![](../../../assets/_blue_star_.png), `Cartfile.private`, `Cartfile.resolved`<br>{% hint style="success" %}<br>At least one `.private` or `.resolved` file must be included.<br>{% endhint %} |

</details>

<details>

<summary>Go</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/6413877449.png) | **Languages/Frameworks:** Go<br>**Repository:** Golang<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with ![](../../../assets/_blue_star_.png) are required) |
| GoModules | | | `go.mod`![](../../../assets/_blue_star_.png), `go.sum` |

</details>

<details>

<summary>Ruby</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/ruby.png) | **Languages/Frameworks:** Ruby<br>**Repository:** RubyGems<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with ![](../../../assets/_blue_star_.png) are required) |
| RubyGems | | | `Gemfile`![](../../../assets/_blue_star_.png), `Gemfile.lock` |
| Bundler | | | |

</details>

<details>

<summary>C++</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/download__1_.png) | **Languages/Frameworks:** C, C++<br>**Repository:** Conan<br>**File Types:** .cpp, .c, .h, .hpp, .a, .o, .so<br>**Exploitable Path:** Not supported<br>{% hint style="success" %}<br>C++ is supported only for File Analysis (fingerprints), not for package resolution.<br>{% endhint %} | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** |
| none | | | none |

</details>

<details>

<summary>Unity</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/Unity_logo_PNG10.png) | **Languages/Frameworks:** Unity<br>**Repository:**[Unity Technologies](https://github.com/orgs/Unity-Technologies/repositories), [Needle-mirror](https://github.com/orgs/needle-mirror/repositories), [Open UPM](https://openupm.com/packages/)<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** (Packages marked with ![](../../../assets/_blue_star_.png) are required) |
| none | | | `manifest.json`![](../../../assets/_blue_star_.png), `packages.json`![](../../../assets/_blue_star_.png) |

</details>

<details>

<summary>Perl</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/Perl_Programming_Language.png) | **Languages/Frameworks:** Perl<br>**Repository:** [Cpan](https://www.cpan.org/)<br>**File Types:** .pl, .pm<br>**Exploitable Path:** Not supported | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** |
| Cpan | | | `cpanfile`, `spcanfile.snapshot` |

</details>

<details>

<summary>Dart</summary>

| | | | |
|---|---|---|---|
| ![](../../../assets/Picture1.jpg) | **Languages/Frameworks:** Dart, Flutter<br>**Repository:** N/A<br>**File Types:** none<br>**Exploitable Path:** Not supported | | |
| **Supported Package Manager** | **Vulnerability Support** | **Malicious Package Support** | **Manifest Files** |
| Pub | <sup>1\]</sup> | | `pubspec.lock` |

1\] Support of Pub is only for identifying malicious packages. Non-malicious packages are not shown at all in the Packages or Risks tabs.

</details>
