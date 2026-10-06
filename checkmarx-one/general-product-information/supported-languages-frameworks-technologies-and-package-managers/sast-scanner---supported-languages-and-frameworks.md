# SAST Scanner - Supported Languages and Frameworks

The Checkmarx SAST scanner currently supports the following languages and frameworks:

{% hint style="info" %}
Checkmarx One currently uses the Engine Pack Version 9.7.7 version of SAST.
{% endhint %}

| **Environment and Primary Languages** | **Secondary Languages** | **Framework** | **File extensions** | **Additional Information** |
|---|---|---|---|---|
| <img src="../../../assets/6022007568.png" alt="" width="102"><br>• Java<br>• J2SE<br>• J2EE | • JSP<br>• JavaScript<br>• VBScript<br>• PL\\SQL<br>• HTML5 | • ATG DSP Taglib<br>• GWT<br>• Hibernate<br>• Google Guice<br>• Java Server Faces (JSF)<br>• JSP<br>• JSTL FMT Taglib<br>• OWASP ESAPI<br>• MyBatis<br>• PrimeFaces<br>• Spring Boot<br>• Spring MVC<br>• Spring<br>• Struts<br>• Velocity | • .java<br>• .jsp<br>• .jspf<br>• .jsf<br>• .tag<br>• .tld<br>• .mf<br>• .xhtml<br>• .vm<br>• .gradle<br>• .properties<br>• .jspdsbld<br>• .wod<br>• .xml<br>• .yml<br>• .yaml | Java can be configured as a unified language with Scala. |
| {% hint style="info" %}<br>The SAST engine supports JSP files. However, JSP custom tag libraries (taglibs) are not currently supported.<br>{% endhint %} | | | | |
| <img src="../../../assets/6022007571.png" alt="" width="150"><br>• C#<br>• [VB.NET](http://VB.NET) | • ASP.NET<br>• JavaScript<br>• VBScript<br>• PL\\SQL<br>• HTML5 | • ASP.NET Core<br>• ASP.Net Core Razor<br>• ASP.Net MVC framework<br>• Enterprise Libraries<br>• ComponentArt<br>• Entity framework<br>• Hibernate.Net<br>• Infragistics<br>• iBatis<br>• Telerik<br>• Dapper<br>• .Net Core<br>• .Net Framework<br>• .NET | • .cs<br>• .cshtml<br>• .xaml<br>• .vb<br>• .config<br>• .aspx<br>• .ascx<br>• .asax<br>• .tag<br>• .master<br>• .xml | |
| <img src="../../../assets/6022007574.png" alt="" width="150"><br>• ASP | • JavaScript \[\*\*\]<br>• VBScript<br>• PL\\SQL<br>• HTML5 | • ASP.Net MVC framework | • .asp<br>• .inc | |
| <img src="../../../assets/6022007577.png" alt="" width="114"><br>• VB6 | | | • .bas<br>• .vbp<br>• .frm<br>• .cls<br>• .dsr<br>• .ctl | |
| <img src="../../../assets/6022007580.png" alt="" width="150"><br>• C<br>• C++ | | • C MISRA<br>• C++ MISRA<br>• Informix ESQL/C<br>• MySQL<br>• Boost library<br>• stdlib library | • .cpp<br>• .c<br>• .cc<br>• .c++<br>• .cxx<br>• .hpp<br>• .hh<br>• .h++<br>• .hxx<br>• .h<br>• .ec<br>• .cmake<br>• .pc<br>• .pro<br>• .ac<br>• .am<br>• .txt (related to CmakeLists)<br>• .ph | |
| <img src="../../../assets/64d4d824681bd.svg" alt="" width="150"><br>• PHP | JavaScript | • bWapp<br>• CakePHP<br>• OWASP ESAPI<br>• Kohana<br>• Symfony<br>• Smarty<br>• Zend | • .php<br>• .php3<br>• .php4<br>• .php5<br>• .phtm<br>• .phtml<br>• .tpl<br>• .ctp<br>• .twig<br>• .inc<br>• .cgi<br>• .env<br>• .ini | |
| <img src="../../../assets/6022007586.png" alt="" width="150"><br>• Apex | | • VisualForce<br>• Lightning (Aura)<br>• Lightning Web Components | • .apex<br>• .apexp<br>• .apxc<br>• .page<br>• .component<br>• .cls<br>• .trigger<br>• .tgr<br>• .object<br>• .report<br>• .workflow<br>• -meta.xml<br>• .xml | This is for Salesforce APEX only. |
| <img src="../../../assets/6022007589.png" alt="" width="150"><br>• Ruby | | • Ruby on Rails | • .rb<br>• .rhtml<br>• .rxml<br>• .rjs<br>• .erb<br>• .cgi<br>• .lock | |
| <img src="../../../assets/6022007592.png" alt="" width="150"><br>• JavaScript<br>• Typescript | | • Ajax<br>• Angular<br>• AngularJS<br>• Backbone<br>• Cordova / PhoneGap<br>• Handlebars<br>• Hapi.JS<br>• JQuery<br>• Knockout<br>• Kony Visualizer<br>• Node.js<br>- Buffer<br>- CryptoJS<br>- ExpressJS<br>- File System<br>- Hapi<br>- Mongodb<br>- OracleDB<br>- Sequelize<br>• Pug (Jade)<br>• React Native<br>• ReactJS<br>• SAPUI5<br>• VueJS<br>• XS (SAP)<br>• RequireJS | • .js<br>• .jsx<br>• .htm<br>• .html<br>• .json<br>• .ts<br>• .tsx<br>• .aspx<br>• .ascx<br>• .xsjs<br>• .xsjslib<br>• .xsaccess<br>• .xsapp<br>• .app<br>• .evt<br>• .cmp<br>• .hbs<br>• .handlebars<br>• .jade<br>• .pug<br>• .vue<br>• .xml<br>• .apexp<br>• .page<br>• .component<br>• .cshtml<br>• .jsf<br>• .xhtml<br>• .jsp<br>• .jspf<br>• .asp<br>• .master<br>• .php | |
| <img src="../../../assets/6022007598.png" alt="" width="150"><br>• VBScript | | | • .vbs<br>• .aspx<br>• .ascx<br>• .asp<br>• .cshtml<br>• .html<br>• .htm<br>• .master | |
| <img src="../../../assets/6022007601.png" alt="" width="150"><br>• Perl | | | • .pl<br>• .pm<br>• .plx<br>• .psgi<br>• .cgi | |
| <img src="../../../assets/6022007604.png" alt="" width="70"><br>• Android (Java) | | • Volley | • .java<br>• .kt | |
| <img src="../../../assets/6022007607.png" alt="" width="150"><br>• Objective-C<br>• Swift | | | • .m<br>• .h<br>• .swift<br>• .xib<br>• .plist | |
| <img src="../../../assets/6022007610.png" alt="" width="50"><br>• HTML 5 | | | • .html<br>• .htm | |
| <img src="../../../assets/6022007613.png" alt="" width="97"><br>• PL/SQL | | | • .pls<br>• .sql<br>• .pkh<br>• .pks<br>• .pkb<br>• .pck | |
| SQL | | | • .sql<br>• .tsql | |
| <img src="../../../assets/6022007616.png" alt="" width="138"><br>• Python | • JavaScript<br>• VB script<br>• PL\\SQL | • Django<br>• Flask<br>• Jinja and DTL<br>• Pandas library<br>• Marshmallow | • .py<br>• .gtl<br>• .csv<br>• .latex<br>• .tex<br>• .html<br>• .xml<br>• .txt | |
| <img src="../../../assets/6022007619.png" alt="" width="150"><br>• Groovy | • JavaScript<br>• VB script<br>• PL\\SQL | | • .groovy<br>• .gsh<br>• .gvy<br>• .gy<br>• .gsp<br>• .gradle | |
| <img src="../../../assets/6022007622.png" alt="" width="150"><br>• Scala | | • Akka<br>• Finagle<br>• Finatra | • .scala<br>• .conf | Scala can be configured as a unified language with Java. |
| <img src="../../../assets/6022007625.png" alt="" width="150"><br>• GO Language | | • Protobuf<br>• gin-gonic/gin<br>• gorilla-mux | • .go<br>• .mod | |
| <img src="../../../assets/kotlinlogo.png" alt="" width="121"><br>• Kotlin | | • Ktor (Server Side)<br>• Vert.x (Server Side)<br>• Spring | • .kt<br>• .kts<br>• .mustache<br>• .ftl<br>• .xml | |
| <img src="../../../assets/6022007508.jpg" alt="" width="150"><br>• Cobol | | | • .cbl<br>• .cob<br>• .eco<br>• .pco<br>• .sqb<br>• .cpy | |
| <img src="../../../assets/6994002109.png" alt="" width="150"><br>• RPG | | | • .rpg<br>• .rpg38<br>• .sqlrpg<br>• .rpgle<br>• .sqlrpgle<br>• .dspf | |
| <img src="../../../assets/6994002106.png" alt="" width="150"><br>• Dart | | • Flutter | • .dart<br>• .yaml | |
| <img src="../../../assets/6993019381.png" alt="" width="150"><br>• Lua | | • OpenResty | • .lua<br>• .conf | |
| <img src="../../../assets/Rust.png" alt="" width="150"><br>• Rust | | | • .rs<br>• .toml | |
