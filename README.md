# internet-speed-test-automatic
This code automatically performs speed tests on all initially listed servers after server selection on speedtest.net and gives a one-star rating in the survey if it appears.

1.  **Go to the developer console code in my repository and copy the code.**
2.  **Open Speedtest.net.**
3.  **Open the developer tools by pressing F12.**
4.  **Click on the "Console" tab.**
5.  **Paste the code and press Enter.**
```markdown
async function testAllInitialServers() {
  try {
    // 1. Sunucu seçme bölümünü aç
    const openServerButton = document.querySelector('.btn-server-select');
    if (openServerButton) {
      openServerButton.click();
      await new Promise(resolve => setTimeout(resolve, 2000)); // Animasyon ve listenin yüklenmesi için bekle
    } else {
      console.error("Sunucu seçme butonu bulunamadı.");
      return;
    }

    // 2. Arama yapmadan doğrudan çıkan sunucuları bul
    const serverListContainer = document.querySelector('.server-hosts .server-hosts-list ul');
    if (!serverListContainer) {
      console.error("Sunucu listesi kapsayıcısı bulunamadı.");
      return;
    }
    let serverItems = serverListContainer.querySelectorAll('li');

    console.log(`Bulunan ilk sunucu sayısı: ${serverItems.length}`);

    for (let i = 0; i < serverItems.length; i++) {
      const serverItem = serverItems[i];
      const serverNameElement = serverItem.querySelector('.host-location');
      const serverName = serverNameElement ? serverNameElement.textContent.trim() : `Bilinmeyen Sunucu ${i + 1}`;
      console.log(`Test ediliyor: ${serverName}`);

      // 3. Sunucuyu seç
      const selectButton = serverItem.querySelector('a');
      if (selectButton) {
        selectButton.click();
        await new Promise(resolve => setTimeout(resolve, 1000)); // Seçim sonrası bekleme
      } else {
        console.warn(`${serverName} için seçme butonu bulunamadı.`);
        continue;
      }

      // 4. Testi başlat
      const startButton = document.querySelector('.js-start-test');
      if (startButton) {
        startButton.click();
        console.log(`${serverName} için test başlatıldı.`);

        // Testin bitmesini bekle
        await waitForTestCompletion();
        console.log(`${serverName} için test tamamlandı.`);

        // 5. Anketi kontrol et ve tıkla (tek yıldız)
        await new Promise(resolve => setTimeout(resolve, 2000)); // Test bittikten sonra anketin görünmesi için biraz daha bekle

        const surveyContainer = document.querySelector('.audience-survey-answers');
        if (surveyContainer) {
          const firstStar = surveyContainer.querySelector('li:first-child a');
          if (firstStar) {
            firstStar.click();
            console.log("Anket (tek yıldız) yanıtlandı.");
            await new Promise(resolve => setTimeout(resolve, 1000)); // Anket sonrası bekleme
          } else {
            console.warn("Anket cevabı (tek yıldız) bulunamadı.");
          }
        } else {
          console.log("Anket alanı bulunamadı.");
        }

        // Son sunucu değilse, bir sonraki sunucuyu test etmek için sunucu seçimini tekrar aç
        if (i < serverItems.length - 1) {
          const reOpenServerButton = document.querySelector('.btn-server-select');
          if (reOpenServerButton) {
            reOpenServerButton.click();
            await new Promise(resolve => setTimeout(resolve, 2000)); // Açılma ve listenin yüklenmesi için bekle

            // Sunucu listesini tekrar bul (yeni liste yüklenmiş olabilir)
            const updatedServerListContainer = document.querySelector('.server-hosts .server-hosts-list ul');
            if (updatedServerListContainer) {
              serverItems = updatedServerListContainer.querySelectorAll('li');
            } else {
              console.warn("Güncellenmiş sunucu listesi bulunamadı.");
              break; // Liste bulunamazsa döngüyü sonlandır
            }
          }
        }
      } else {
        console.error("Test başlatma butonu bulunamadı.");
        return;
      }
    }

    console.log("Tüm ilk sunucular test edildi.");

  } catch (error) {
    console.error("Bir hata oluştu:", error);
  }
}

// Testin bitmesini bekleyen basit bir fonksiyon
async function waitForTestCompletion() {
  return new Promise(resolve => {
    console.log("Testin bitmesi bekleniyor...");
    setTimeout(resolve, 45000); // Örnek olarak 45 saniye bekleniyor.
  });
}

testAllInitialServers();
```

**Almanca:**

```markdown
# internet-speed-test-automatic
Dieser Code führt automatisch Geschwindigkeitstests auf allen anfänglich aufgelisteten Servern nach der Serverauswahl auf speedtest.net durch und gibt im Falle einer Umfrage eine Ein-Sterne-Bewertung ab.
```

**Fransız:**

```markdown
# internet-speed-test-automatic
Ce code effectue automatiquement des tests de vitesse sur tous les serveurs initialement listés après la sélection du serveur sur speedtest.net et attribue une note d'une étoile dans le sondage s'il apparaît.
```

**İspanyolca:**

```markdown
# internet-speed-test-automatic
Este código realiza automáticamente pruebas de velocidad en todos los servidores listados inicialmente después de la selección del servidor en speedtest.net y otorga una calificación de una estrella en la encuesta si aparece.
```

**İtalyanca:**

```markdown
# internet-speed-test-automatic
Questo codice esegue automaticamente test di velocità su tutti i server elencati inizialmente dopo la selezione del server su speedtest.net e assegna una valutazione di una stella nel sondaggio se appare.
```

**Rusça:**

```markdown
# internet-speed-test-automatic
Этот код автоматически выполняет тесты скорости на всех первоначально перечисленных серверах после выбора сервера на speedtest.net и ставит одну звезду в опросе, если он появляется.
```

**Japonca:**

```markdown
# internet-speed-test-automatic
このコードは、speedtest.net でサーバー選択後に最初にリスト表示されたすべてのサーバーで自動的に速度テストを実行し、アンケートが表示された場合は 1 つ星の評価を付けます。
```

**Çince (Basitleştirilmiş):**

```markdown
# internet-speed-test-automatic
此代码在 speedtest.net 上选择服务器后，自动对所有初始列出的服务器执行速度测试，并在出现调查问卷时给予一星评级。
```

**Arapça:**

```markdown
# internet-speed-test-automatic
يقوم هذا الكود تلقائيًا بإجراء اختبارات السرعة على جميع الخوادم المدرجة مبدئيًا بعد اختيار الخادم على موقع speedtest.net ويمنح تقييمًا بنجمة واحدة في الاستطلاع إذا ظهر.
```

**Portekizce:**

```markdown
# internet-speed-test-automatic
Este código executa automaticamente testes de velocidade em todos os servidores listados inicialmente após a seleção do servidor no speedtest.net e atribui uma classificação de uma estrela na pesquisa, se aparecer.
```

**Hollandaca:**

```markdown
# internet-speed-test-automatic
Deze code voert automatisch snelheidstests uit op alle initieel vermelde servers na de serverselectie op speedtest.net en geeft een beoordeling van één ster in de enquête als deze verschijnt.
```

**Lehçe:**

```markdown
# internet-speed-test-automatic
Ten kod automatycznie wykonuje testy prędkości na wszystkich początkowo wymienionych serwerach po wybraniu serwera na speedtest.net i przyznaje ocenę jednej gwiazdki w ankiecie, jeśli się pojawi.
```

**İsveççe:**

```markdown
# internet-speed-test-automatic
Den här koden utför automatiskt hastighetstester på alla initialt listade servrar efter serverval på speedtest.net och ger ett stjärnbetyg i undersökningen om den visas.
```

**Yunanca:**

```markdown
# internet-speed-test-automatic
Αυτός ο κώδικας εκτελεί αυτόματα δοκιμές ταχύτητας σε όλους τους αρχικά αναγραφόμενους διακομιστές μετά την επιλογή διακομιστή στο speedtest.net και δίνει μια βαθμολογία ενός αστεριού στην έρευνα αν εμφανιστεί.
```

**Korece:**

```markdown
# internet-speed-test-automatic
이 코드는 speedtest.net에서 서버를 선택한 후 처음에 나열된 모든 서버에서 자동으로 속도 테스트를 수행하고 설문 조사가 나타나면 별 하나 등급을 부여합니다.
```

**Vietnamca:**

```markdown
# internet-speed-test-automatic
Mã này tự động thực hiện kiểm tra tốc độ trên tất cả các máy chủ được liệt kê ban đầu sau khi chọn máy chủ trên speedtest.net và đưa ra xếp hạng một sao trong khảo sát nếu nó xuất hiện.
```

**Tayca:**

```markdown
# internet-speed-test-automatic
รหัสนี้จะดำเนินการทดสอบความเร็วโดยอัตโนมัติบนเซิร์ฟเวอร์ที่แสดงรายการเริ่มต้นทั้งหมดหลังจากเลือกเซิร์ฟเวอร์บน speedtest.net และให้คะแนนหนึ่งดาวในการสำรวจหากปรากฏขึ้น
```

**Endonezyaca:**

```markdown
# internet-speed-test-automatic
Kode ini secara otomatis melakukan uji kecepatan pada semua server yang terdaftar pada awalnya setelah pemilihan server di speedtest.net dan memberikan peringkat bintang satu dalam survei jika muncul.
```

**Hintçe:**

```markdown
# internet-speed-test-automatic
यह कोड speedtest.net पर सर्वर चयन के बाद शुरू में सूचीबद्ध सभी सर्वरों पर स्वचालित रूप से गति परीक्षण करता है और यदि सर्वेक्षण दिखाई देता है तो एक-स्टार रेटिंग देता है।
```

1.  **Depomdaki developer console code gidip kodu kopyalayın.**
2.  **Speedtest.net'i açın.**
3.  **F12'ye basarak geliştirici araçlarını açın.**
4.  **"Console" sekmesine tıklayın.**
5.  **Kodu yapıştırıp Enter'a basın.**

**İngilizce:**

1.  **Go to the developer console code in my repository and copy the code.**
2.  **Open Speedtest.net.**
3.  **Open the developer tools by pressing F12.**
4.  **Click on the "Console" tab.**
5.  **Paste the code and press Enter.**

**Almanca:**

1.  **Gehen Sie zum Entwicklerkonsolen-Code in meinem Repository und kopieren Sie den Code.**
2.  **Öffnen Sie Speedtest.net.**
3.  **Öffnen Sie die Entwicklertools, indem Sie F12 drücken.**
4.  **Klicken Sie auf die Registerkarte "Konsole".**
5.  **Fügen Sie den Code ein und drücken Sie die Eingabetaste.**

**Fransız:**

1.  **Allez au code de la console développeur dans mon dépôt et copiez le code.**
2.  **Ouvrez Speedtest.net.**
3.  **Ouvrez les outils de développement en appuyant sur F12.**
4.  **Cliquez sur l'onglet "Console".**
5.  **Collez le code et appuyez sur Entrée.**

**İspanyolca:**

1.  **Ve al código de la consola de desarrollador en mi repositorio y copia el código.**
2.  **Abre Speedtest.net.**
3.  **Abre las herramientas de desarrollo presionando F12.**
4.  **Haz clic en la pestaña "Consola".**
5.  **Pega el código y presiona Enter.**

**İtalyanca:**

1.  **Vai al codice della console per sviluppatori nel mio repository e copia il codice.**
2.  **Apri Speedtest.net.**
3.  **Apri gli strumenti per sviluppatori premendo F12.**
4.  **Fai clic sulla scheda "Console".**
5.  **Incolla il codice e premi Invio.**

**Rusça:**

1.  **Перейдите к коду консоли разработчика в моем репозитории и скопируйте код.**
2.  **Откройте Speedtest.net.**
3.  **Откройте инструменты разработчика, нажав F12.**
4.  **Нажмите на вкладку "Консоль".**
5.  **Вставьте код и нажмите Enter.**

**Japonca:**

1.  **私のリポジトリにある開発者コンソールコードに移動し、コードをコピーしてください。**
2.  **Speedtest.net を開きます。**
3.  **F12 キーを押して開発者ツールを開きます。**
4.  **「コンソール」タブをクリックします。**
5.  **コードを貼り付けて Enter キーを押します。**

**Çince (Basitleştirilmiş):**

1.  **转到我存储库中的开发者控制台代码并复制该代码。**
2.  **打开 Speedtest.net。**
3.  **按 F12 打开开发者工具。**
4.  **单击“控制台”选项卡。**
5.  **粘贴代码并按 Enter 键。**

**Arapça:**

1.  **انتقل إلى كود وحدة تحكم المطور في مستودعي وانسخ الكود.**
2.  **افتح موقع Speedtest.net.**
3.  **افتح أدوات المطور بالضغط على F12.**
4.  **انقر على علامة التبويب "وحدة التحكم".**
5.  **الصق الكود واضغط على مفتاح الإدخال (Enter).**

Elbette, işte birkaç dil daha eklenmiş hali:

**Portekizce:**

1.  **Vá para o código do console do desenvolvedor no meu repositório e copie o código.**
2.  **Abra o Speedtest.net.**
3.  **Abra as ferramentas de desenvolvedor pressionando F12.**
4.  **Clique na guia "Console".**
5.  **Cole o código e pressione Enter.**

**Hollandaca:**

1.  **Ga naar de code van de ontwikkelaarsconsole in mijn repository en kopieer de code.**
2.  **Open Speedtest.net.**
3.  **Open de ontwikkelaarstools door op F12 te drukken.**
4.  **Klik op het tabblad "Console".**
5.  **Plak de code en druk op Enter.**

**Lehçe:**

1.  **Przejdź do kodu konsoli dewelopera w moim repozytorium i skopiuj kod.**
2.  **Otwórz Speedtest.net.**
3.  **Otwórz narzędzia deweloperskie, naciskając F12.**
4.  **Kliknij kartę "Konsola".**
5.  **Wklej kod i naciśnij Enter.**

**İsveççe:**

1.  **Gå till utvecklarkonsolens kod i mitt arkiv och kopiera koden.**
2.  **Öppna Speedtest.net.**
3.  **Öppna utvecklarverktygen genom att trycka på F12.**
4.  **Klicka på fliken "Konsol".**
5.  **Klistra in koden och tryck på Enter.**

**Yunanca:**

1.  **Μεταβείτε στον κώδικα της κονσόλας προγραμματιστή στο αποθετήριό μου και αντιγράψτε τον κώδικα.**
2.  **Ανοίξτε το Speedtest.net.**
3.  **Ανοίξτε τα εργαλεία προγραμματιστή πατώντας F12.**
4.  **Κάντε κλικ στην καρτέλα "Κονσόλα".**
5.  **Επικολλήστε τον κώδικα και πατήστε Enter.**

**Korece:**

1.  **내 리포지토리의 개발자 콘솔 코드로 이동하여 코드를 복사하십시오.**
2.  **Speedtest.net을 엽니다.**
3.  **F12 키를 눌러 개발자 도구를 엽니다.**
4.  **"콘솔" 탭을 클릭하십시오.**
5.  **코드를 붙여넣고 Enter 키를 누르십시오.**

**Vietnamca:**

1.  **Truy cập mã bảng điều khiển nhà phát triển trong kho lưu trữ của tôi và sao chép mã.**
2.  **Mở Speedtest.net.**
3.  **Mở công cụ dành cho nhà phát triển bằng cách nhấn F12.**
4.  **Nhấp vào tab "Bảng điều khiển".**
5.  **Dán mã và nhấn Enter.**

**Tayca:**

1.  **ไปที่โค้ดคอนโซลสำหรับนักพัฒนาในที่เก็บของฉันและคัดลอกโค้ด**
2.  **เปิด Speedtest.net**
3.  **เปิดเครื่องมือสำหรับนักพัฒนาโดยกด F12**
4.  **คลิกแท็บ "คอนโซล"**
5.  **วางโค้ดแล้วกด Enter**

**Endonezyaca:**

1.  **Buka kode konsol pengembang di repositori saya dan salin kodenya.**
2.  **Buka Speedtest.net.**
3.  **Buka alat pengembang dengan menekan F12.**
4.  **Klik tab "Konsol".**
5.  **Tempel kode dan tekan Enter.**

**Hintçe:**

1.  **मेरे रिपॉजिटरी में डेवलपर कंसोल कोड पर जाएँ और कोड कॉपी करें।**
2.  **Speedtest.net खोलें।**
3.  **F12 दबाकर डेवलपर टूल खोलें।**
4.  **"कंसोल" टैब पर क्लिक करें।**
5.  **कोड पेस्ट करें और एंटर दबाएँ।**
