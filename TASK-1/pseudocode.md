// atm.dot — ATM para çekme akışı (Graphviz DOT)
digraph ATM {
  rankdir=TB;                     // yukarıdan aşağı akış
  node [fontname="Helvetica"];
  
  // düğüm stilleri
  Start [label="Başla", shape=circle, style=filled, fillcolor="#e6f7ff"];
  InsertCard [label="Kartı tak", shape=box];
  ReadCard [label="Kartı oku / kimlik doğrula", shape=box];
  EnterPIN [label="PIN gir", shape=box];
  CheckPIN [label="PIN doğru mu?", shape=diamond];
  PIN_Incorrect [label="Yanlış PIN", shape=box];
  PIN_Attempts [label="PIN deneme sayısı++", shape=box];
  RetainCard [label="Kartı tut (3 yanlış)", shape=box, style=filled, fillcolor="#ffe6e6"];
  
  MainMenu [label="İşlem seç (Para Çekme / Diğer)", shape=box];
  SelectWithdrawal [label="Para Çekme seçildi mi?", shape=diamond];
  EnterAmount [label="Çekilecek tutarı gir", shape=box];
  CheckBalance [label="Hesapta yeterli para var mı?", shape=diamond];
  CheckATM [label="ATM'de yeterli nakit var mı?", shape=diamond];
  DispenseCash [label="Parayı ver (fiş opc.)", shape=box, style=filled, fillcolor="#e6ffe6"];
  UpdateAccount [label="Hesap bakiyesini güncelle", shape=box];
  EjectCard [label="Kartı ver / çıkış", shape=box];
  PrintReceipt [label="Fiş yazdır (isteğe bağlı)", shape=box];
  End [label="Bitiş", shape=circle, style=filled, fillcolor="#e6f7ff"];
  
  InsufficientFunds [label="Yetersiz bakiye -> Hata mesajı", shape=box, style=filled, fillcolor="#fff0e6"];
  InsufficientATM [label="ATM'de yetersiz nakit -> Hata mesajı", shape=box, style=filled, fillcolor="#fff0e6"];
  Cancelled [label="İşlem iptal edildi", shape=box];
  
  // kenarlar (akış)
  Start -> InsertCard -> ReadCard -> EnterPIN -> CheckPIN;
  
  CheckPIN -> EnterAmount [label="PIN doğru", style=solid, fontsize=10, tailport=s, headport=n];
  CheckPIN -> PIN_Incorrect [label="PIN yanlış", style=dashed];
  
  PIN_Incorrect -> PIN_Attempts -> CheckPIN [label="3'ten az ise tekrar PIN iste", style=dotted];
  PIN_Attempts -> RetainCard [label="3 ise", style=bold];
  RetainCard -> End;
  
  EnterAmount -> SelectWithdrawal [label="(akışı devam ettir)"];
  SelectWithdrawal -> MainMenu [label="Evet: Para Çekme değilse menüye", style=dotted];
  MainMenu -> SelectWithdrawal;
  
  SelectWithdrawal -> EnterAmount [label="Evet", style=solid];
  EnterAmount -> CheckBalance;
  
  CheckBalance -> InsufficientFunds [label="Hayır", style=dashed];
  InsufficientFunds -> EjectCard -> End;
  
  CheckBalance -> CheckATM [label="Evet"];
  CheckATM -> InsufficientATM [label="Hayır"];
  InsufficientATM -> Cancelled -> EjectCard -> End;
  
  CheckATM -> DispenseCash [label="Evet"];
  DispenseCash -> UpdateAccount -> PrintReceipt -> EjectCard -> End;
  
  // iptal ve zaman aşımı yolları
  EnterPIN -> Cancelled [label="Kullanıcı iptal etti", style=dotted];
  EnterAmount -> Cancelled [label="Kullanıcı iptal etti", style=dotted];
  Cancelled -> EjectCard;
  
  // görsel düzenleme
  { rank = same; DispenseCash UpdateAccount PrintReceipt }
}
