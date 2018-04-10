### <a name="rsacng-and-dsacng-are-once-again-usable-in-partial-trust-scenarios"></a>RSACng und DSACng werden in teilweise vertrauenswürdigen Szenarien erneut verwendet können

|   |   |
|---|---|
|Details|CngLightup (verwendet in mehrere auf höherer Ebene Crypto-apis, wie z. B. <xref:System.Security.Cryptography.Xml.EncryptedXml?displayProperty=nameWithType>) und <xref:System.Security.Cryptography.RSACng?displayProperty=nameWithType> in einigen Fällen sind auf volle Vertrauenswürdigkeit. Dazu gehören P/Invokes ohne Bestätigung <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode?displayProperty=nameWithType> Berechtigungen und Codepfade, in denen <xref:System.Security.Cryptography.CngKey?displayProperty=nameWithType> verfügt über die Berechtigung Forderungen nach <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode?displayProperty=nameWithType>. Beginnend mit .NET Framework 4.6.2, CngLightup wurde verwendet, um zu wechseln <xref:System.Security.Cryptography.RSACng?displayProperty=nameWithType> möglichst. Folglich teilweise vertrauenswürdigen apps, die erfolgreich verwendet <xref:System.Security.Cryptography.Xml.EncryptedXml?displayProperty=nameWithType> begonnen hat, schlägt fehl, und lösen <xref:System.Security.SecurityException> Ausnahmen. Diese Änderung hinzugefügt, dass die erforderlichen Assertionen, damit alle Funktionen CngLightup über die erforderlichen Berechtigungen verfügen.|
|Vorschlag|Wenn diese Änderung in .NET Framework 4.6.2 teilweiser Vertrauenswürdigkeit apps beeinträchtigt ist, aktualisieren Sie auf das .NET Framework 4.7.1.|
|Bereich|Edge|
|Version|4.6.2|
|Typ|Laufzeit|
|Betroffene APIs|<ul><li><xref:System.Security.Cryptography.DSACng.%23ctor(System.Security.Cryptography.CngKey)?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.DSACng.Key?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.DSACng.LegalKeySizes?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.DSACng.CreateSignature(System.Byte[])?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.DSACng.VerifySignature(System.Byte[],System.Byte[])?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RSACng.%23ctor(System.Security.Cryptography.CngKey)?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RSACng.Key?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RSACng.Decrypt(System.Byte[],System.Security.Cryptography.RSAEncryptionPadding)?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RSACng.SignHash(System.Byte[],System.Security.Cryptography.HashAlgorithmName,System.Security.Cryptography.RSASignaturePadding)?displayProperty=nameWithType></li></ul>|
