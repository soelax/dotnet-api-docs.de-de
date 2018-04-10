### <a name="new-64-bit-jit-compiler-in-the-net-framework-46"></a>Neue 64-Bit-JIT-Compiler in .NET Framework 4.6

|   |   |
|---|---|
|Details|Ab .NET Framework 4.6 wird ein neuer 64-Bit-JIT-Compiler für die Just-in-Time-Kompilierung verwendet. In einigen Fällen eine unerwartete Ausnahme ausgelöst wird, oder ein anderes Verhalten als eingehalten wird, wenn eine app mit der 32-Bit-Compiler oder der älteren 64-Bit-JIT-Compiler ausgeführt wird. Diese Änderung wirkt sich nicht auf die 32-Bit-JIT-Compiler aus. Die bekannten Unterschiede umfassen Folgendes:<ul><li>Unter bestimmten Umständen kann ein Unboxingvorgang in Releasebuilds mit aktivierter Optimierung eine <xref:System.NullReferenceException>-Ausnahme auslösen.</li><li>In manchen Fällen kann bei der Ausführung von Produktionscode in einem großen Methodentext eine <xref:System.StackOverflowException>-Ausnahme ausgelöst werden.</li><li>Strukturen, die an eine Methode übergeben werden unter bestimmten Umständen kann als Verweistypen behandelt, anstatt als Wert in Version Typen erstellt. Eins der Anzeichen dieses Problems besteht darin, dass die einzelnen Elemente einer Sammlung in unerwarteter Reihenfolge angezeigt werden.</li><li>Unter bestimmten Bedingungen ist der Vergleich von <xref:System.UInt16>-Werten mit festgelegtem hohem Bit fehlerhaft, wenn Optimierung aktiviert ist.</li><li>Unter bestimmten Umständen, insbesondere beim Initialisieren von Arraywerten, kann die Speicherinitialisierung durch die IL-Anweisung <xref:System.Reflection.Emit.OpCodes.Initblk?displayProperty=nameWithType> mit einem falschen Wert erfolgen. Dies kann entweder zu einem Ausnahmefehler oder zu einer falschen Ausgabe führen.</li><li>Unter bestimmten seltenen Bedingungen kann ein bedingter Bittest den falschen <xref:System.Boolean>-Wert zurückgeben oder eine Ausnahme auslösen, wenn Compileroptimierungen aktiviert sind.</li><li>Wenn unter bestimmten Umständen eine <code>if</code>-Anweisung für die Prüfung auf eine Bedingung vor dem Eintritt in einen <code>try</code>-Block oder beim Verlassen eines <code>try</code>-Blocks erfolgt und die gleiche Bedingung im <code>catch</code>- oder <code>finally</code>-Block ausgewertet wird, entfernt der neue 64-Bit-JIT-Compiler beim Optimieren von Code die <code>if</code>-Bedingung aus dem <code>catch</code>- oder <code>finally</code>-Block. Daher wird Code innerhalb der <code>if</code>-Anweisung im <code>catch</code>- oder <code>finally</code>-Block ohne Bedingung ausgeführt.</li></ul>|
|Vorschlag|<strong>Minderung der bekannten Probleme</strong> Wenn Sie die oben aufgeführten Probleme auftreten, können Sie sie beheben, indem Sie eine der folgenden Aktionen:<ul><li>Ausführen eines Upgrades auf .NET Framework 4.6.2. Der neue 64-Bit-Compiler, der in .NET Framework 4.6.2 enthalten ist, behebt jedes dieser bekannten Probleme.</li><li>Stellen Sie sicher, dass ihre Windows-Version auf dem aktuellen Stand ist, indem Sie Windows Update ausführen. Serviceupdates für .NET Framework 4.6 und 4.6.1 beheben jedes dieser Probleme, mit Ausnahme der <xref:System.NullReferenceException>-Ausnahme bei Unboxingvorgängen.</li><li>Kompilieren Sie mit dem älteren 64-Bit-JIT-Compiler. Informationen zum Vorgehen dazu finden Sie unter <strong>Entschärfung anderer Probleme</strong>.</li></ul><strong>Abwehr von anderen Problemen</strong> treten keine andere Unterschiede im Verhalten zwischen Code, der mit der älteren 64-Bit-Compiler und der neue 64-Bit-JIT-Compiler kompiliert, und zwischen den Versionen Debug- und Releasebuilds Ihrer App, die sowohl mit dem neuen kompiliert 64-Bit-JIT-Compiler, erreichen Sie Folgendes ein, um die app mit der älteren 64-Bit-JIT-Compiler kompilieren:<ul><li>Sie können der Konfigurationsdatei Ihrer Anwendung auf Anwendungsbasis das [\<useLegacyJit>](~/docs/framework/configure-apps/file-schema/runtime/uselegacyjit-element.md)-Element hinzufügen. Die folgende Anweisung deaktiviert die Kompilierung mit dem neuen 64-Bit-JIT-Compiler und verwendet stattdessen den 64-Bit-Legacy-JIT-Compiler.</li></ul><pre><code class="language-xml">&lt;?xml version =&quot;1.0&quot;?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;useLegacyJit enabled=&quot;1&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre><ul><li>Auf Benutzerbasis können Sie dem <code>HKEY_CURRENT_USER\SOFTWARE\Microsoft\.NETFramework</code>-Wert der Registrierung einen <code>REG_DWORD</code>-Wert mit dem Namen <code>useLegacyJit</code> hinzufügen. Der Wert 1 aktiviert den 64-Bit-Legacy-JIT-Compiler, der Wert 0 deaktiviert ihn und aktiviert stattdessen den neuen 64-Bit-JIT-Compiler.</li><li>Auf Computerbasis können Sie dem <code>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework</code>-Schlüssel der Registrierung einen <code>REG_DWORD</code>-Wert mit dem Namen <code>useLegacyJit</code> hinzufügen. Der Wert <code>1</code> ermöglicht die legacy-64-Bit-JIT-Compiler, der Wert <code>0</code> wird deaktiviert, und den neue 64-Bit-JIT-Compiler ermöglicht.</li></ul>Ferner können Sie uns über das Problem informieren, indem Sie einen Bug auf [Microsoft Connect](https://connect.microsoft.com/VisualStudio) melden.|
|Bereich|Edge|
|Version|4.6|
|Typ|Neuzuweisung|
