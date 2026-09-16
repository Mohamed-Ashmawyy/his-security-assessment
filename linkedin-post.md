# LinkedIn Post — Suggested Copy

## English Version

I’m pleased to share a sanitized portfolio summary of an authorized web application and API security assessment I completed for a healthcare information system.

The assessment focused on authentication and authorization controls, privilege escalation, excessive administrative data exposure, client-side secret handling, production diagnostics, and sensitive account-management workflows.

Key areas of work included:

- Manual authenticated testing with controlled role-based accounts.
- Validation of broken function-level authorization and privilege-escalation paths.
- Review of API object-level and field-level access controls.
- Identification of hardcoded credentials in publicly served frontend assets.
- Risk classification using OWASP, CWE, PTES, and CVSS v3.1.
- Development of prioritized remediation and retest criteria.

The most important lesson was that authentication is not authorization. Every privileged read and write operation must enforce its own server-side authorization policy, and no secret should ever be embedded in a client-side bundle.

For confidentiality and responsible disclosure, this portfolio version excludes the client identity, production URL, credentials, tokens, personal data, raw evidence, and exploit-ready details.

#CyberSecurity #WebSecurity #APISecurity #PenetrationTesting #ApplicationSecurity #OWASP #EthicalHacking

## Arabic Version

سعيد بمشاركة ملخص منقح وآمن لأحد مشاريع اختبار اختراق تطبيق ويب وواجهات API لنظام معلومات صحي، مع الالتزام بسرية العميل ومبادئ الإفصاح المسؤول.

ركز التقييم على صلاحيات الوصول، تصعيد الامتيازات، كشف البيانات الإدارية، حماية الأسرار داخل ملفات الواجهة الأمامية، إعدادات التشخيص في بيئة الإنتاج، ومسارات إنشاء الحسابات الحساسة.

شمل العمل اختبارًا يدويًا باستخدام حسابات تجريبية محددة الصلاحيات، وتحليلًا لسلوك واجهات API، وتصنيفًا للمخاطر وفق OWASP وCWE وPTES وCVSS v3.1، بالإضافة إلى إعداد خطة إصلاح ومعايير إعادة اختبار.

أهم درس من المشروع هو أن تسجيل الدخول لا يعني امتلاك صلاحية تنفيذ كل العمليات. يجب أن تفرض الخوادم صلاحيات مستقلة لكل عملية حساسة، كما يجب ألا تحتوي ملفات الواجهة الأمامية على أي كلمات مرور أو أسرار.

تم حذف هوية العميل ورابط النظام وبيانات الدخول والـtokens والبيانات الشخصية والأدلة الخام من النسخة المنشورة.

#الأمن_السيبراني #اختبار_الاختراق #أمن_التطبيقات #أمن_واجهات_API
