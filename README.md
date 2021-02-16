**PULL REQUESTS are appreciated.**

#### English

CoinTaxman helps you to bring your income from crypto trading, lending, ... into your tax declaration.
At the moment CoinTaxman only covers my area of ​​application, pull requests are welcome.

#### German - Deutsch

CoinTaxman hilft dir dabei deine Einkünfte aus dem Krypto-Handel/-Verleih/... in die Steuererklärung zu bringen.
Momentan deckt der CoinTaxman nur meinen Anwendungsbereich ab, Pull Requests sind gerne gesehen.

**Disclaimer: use at your own risk**

### Currently supported countries
- Germany

### Currently supported exchanges
- Binance

### Requirements

- Python 3.9
- See `requirements.txt` for the required modules.
Quick and easy installation can be done with `pip`.
> `pip install -r requirements.txt`

### Usage

1. Adjust `src/config.py` to your likeing
2. Add account statements from supported exchanges in `account_statements/`
2. Run `python "src/main.py"`

### Key notes for developers

#### Adding a new country

- Add your country  to the Country enum in `src/core.py`
- Extend `src/config.py` to fit your tax regulation
- Add a country specific tax evaluation function in `src/taxman.py` like `Taxman._evaluate_taxation_GERMANY`
- Depending on your specific tax regulation, you might need to add additional functionality and might want to add or edit the enums in `src/core.py`

#### Adding a new exchange

- Add a read-in function like `Book._read_binance` in `src/book.py`
- Add a way to retrieve price data from this exchange in `src/price_data.py` like `PriceData._get_price_binance`

# Ideas on crypto-taxation

The taxation of crytocurrency is probably not yet regulated down to the smallest detail in every country. Often there still seem to be ambiguities or gray areas.
This section should help you to dig deeper into the subject.
Feel free to commit details about the taxation in your country.

## Taxation in Germany

Meine Interpretation rund um die Besteuerung von Kryptowährung in Deutschland wird durch die Texte von den [Rechtsanwälten und Steuerberatern WINHELLER](https://www.winheller.com/) sehr gut artikuliert.
Meine kurzen Zusammenfassungen am Ende von jedem Abschnitt werden durch einen ausführlicheren Text von [WINHELLER](https://www.winheller.com/) ergänzt.

An dieser Stelle sei explizit erwähnt, dass dies meine Interpretation ist. Es ist weder sichergestellt, dass ich aktuell noch nach diesen praktiziere (falls ich das Repo in Zukunft nicht mehr aktiv pflege), noch ob diese Art der Versteuerung gesetzlich zulässig ist.
Meine Interpretation steht gerne zur Debatte.

### Allgemein

> Kryptowährungen sind kein gesetzliches Zahlungsmittel. Vielmehr werden sie – zumindest im Ertragsteuerrecht – als immaterielle Wirtschaftsgüter betrachtet. 
>
> Wird der An- und Verkauf von Kryptowährungen als Privatperson unternommen, sind § 22 Nr. 2, § 23 Abs. 1 Nr. 2 EStG einschlägig. Es handelt sich hierbei um ein privates Veräußerungsgeschäft von „anderen Wirtschaftsgütern“. Gemäß § 23 Abs. 3 Satz 1 EStG ist der Gewinn oder Verlust der Unterschied zwischen Veräußerungspreis einerseits und den Anschaffungs- und Werbungskosten andererseits. Es muss also nur der Anschaffungspreis vom Veräußerungspreis abgezogen werden. Die Gebühren beim Handel auf den Börsen sind Werbungskosten und damit abzugsfähig.
>
> In § 23 Abs. 3 Satz 5 EStG ist zudem eine Freigrenze von 600 € vorgesehen, bis zu deren Erreichen alle privaten Veräußerungsgeschäfte des Veranlagungszeitraums steuerfrei bleiben. Wird die Grenze überschritten, muss allerdings der gesamte Betrag ab dem ersten Euro versteuert werden. Die Einkommensteuer fällt dabei nicht erst beim Umtausch von Kryptowährungen in Euro oder eine andere Fremdwährung an, sondern bereits bei einem Tausch in eine beliebige andere Kryptowährung oder auch beim Kauf von Waren oder Dienstleistungen mit einer solchen. Vergeht aber zwischen Anschaffung und Veräußerung mehr als ein Jahr (ggf. zehn Jahre nach § 23 Abs. 1 Nr. 2 Satz 4 EStG), greift die Haltefrist des § 23 Abs. 1 Nr. 2 Satz 1 EStG. In diesen Fällen ist der gesamte Veräußerungsgewinn nicht steuerbar.  
>
> Zur Bestimmung der Anschaffungskosten und des Veräußerungsgewinns sowie zur Bestimmung der Einhaltung der Haltefrist wird in der Regel die sogenannte FIFO-Methode aus § 23 Abs. 1 Nr. 2 Satz 3 EStG herangezogen. Zwar schreibt das Gesetz diese First-In-First-Out-Methode nicht für Kryptowährungen vor, in der Praxis wird sie aber weitgehend angewendet. Es werden allerdings auch andere Meinungen vertreten und eine Berechnung nach der LIFO-Methode oder – zur Bestimmung der Anschaffungskosten – nach Durchschnittswerten vorgeschlagen.

[Quelle](https://www.winheller.com/bankrecht-finanzrecht/bitcointrading/bitcoinundsteuer/besteuerung-kryprowaehrungen.html)
[Wörtlich zitiert vom 14.02.2021]

Zusammenfassung in meinen Worten:
- Kryptowährung sind immaterielle Wirtschaftsgüter.
- Der Verkauf innerhalb eines Jahres gilt als privates Veräußerungsgeschäft und ist als Sonstiges Einkommen zu versteuern (Freigrenze 600 €).
- Der Tausch von Kryptowährung wird ebenfalls versteuert.
- Gebühren zum Handel sind steuerlich abzugsfähig.
- Es kann einmalig entschieden werden, ob nach FIFO oder LIFO versteuert werden soll.

### Airdrops

> Im Rahmen eines Airdrops erhält der Nutzer Kryptowährungen, ohne diese angeschafft oder eine sonstige Leistung hierfür erbracht zu haben. Die Kryptowährungen werden nicht aus dem Rechtskreis eines Dritten auf den Nutzer übertragen. Vielmehr beginnen sie ihre „Existenz“ überhaupt erst in dessen Vermögen. Die Kryptowährung entsteht direkt in den Wallets der Nutzer, wobei die Wallets bestimmte Kriterien erfüllen müssen. Airdrops ähneln insofern einem Lottogewinn oder einem Zufallsfund (sog. Windfall Profits).
>
> Mangels Anschaffungsvorgangs kommt bei einer anschließenden Veräußerung eine Besteuerung nach § 23 Abs. 1 Nr. 2 Einkommensteuergesetz (EStG) nicht in Betracht. Mangels Leistungserbringung seitens des Nutzers liegen auch keine sonstigen Einkünfte i.S.d. § 22 Nr. 3 EStG vor. Damit ist der Verkauf von Airdrops steuerfrei.

[Quelle](https://www.winheller.com/bankrecht-finanzrecht/bitcointrading/bitcoinundsteuer/besteuerung-airdrops.html)
[Wörtlich zitiert vom 14.02.2021]

Zusammenfassung in meinen Worten:
- Erhalt und Verkauf von Airdrops ist steuerfrei.

### Coin Lending

> Handelt es sich bei den durch Krypto-Lending erhaltenen Zinserträgen um Einkünfte aus sonstigen Leistungen gem. § 22 Nr. 3 EStG, so gilt eine Freigrenze von 256 Euro. Beträge darüber werden mit dem perönlichen Einkommensteuersatz von 18 bis 45 % versteuert. Außerdem wäre die spätere Veräußerung gem. § 23 Abs. 1 Nr. 2 EStG der durch das Lending erlangten Kryptowährung mangels Anschaffungsvorgangs nicht steuerbar.
>
> In Deutschland ist die Besteuerung der durch das Krypto-Lending erhaltenen Zinsen jedoch nicht abschließend geklärt. Zum einem wird diskutiert, ob es sich dabei um Kapitaleinkünfte gem. § 20 Abs. 1 Nr. 7 EStG handelt, da es sich bei der Hingabe der Kryptowährung um ein klassisches, verzinsliches Darlehen handelt. Anderseits wird von Finanzämtern immer wieder angenommen, dass es sich bei den erzielten Zinserträgen durch Lending um Einkünfte aus sonstigen Leistungen gem. § 22 Nr. 3 EStG handelt.
>
> Die erhaltene Kryptowährung in Form von Zinsen ist im Zeitpunkt des Zuflusses zu bewerten. Es handele sich deshalb nicht um Kapitaleinkünfte, da die Hingabe der Kryptowährung gerade keine Hingabe von Kapital, sondern vielmehr eine Sachleistung darstelle. Begründet wird dies damit, dass sich eine Kapitalforderung auf eine Geldleistung beziehen muss, nicht aber auf eine Sachleistung, wie es bei Kryptowährungen der Fall ist.
>
> Kontrovers diskutiert wird auch, ob der Verleih einer Kryptowährung zu einer Verlängerung der Haltefrist nach § 23 Abs. 1 Nr. 2 Satz 4 EStG führt. Eine Verlängerung der Haltefrist tritt danach nur dann ein, wenn ein Wirtschaftsgut
> - nach dem 31.12.08 angeschafft wurde,
> - als Einkunftsquelle genutzt wird und
> - damit Einkünfte erzielt werden.
> Unter Nutzung als Einkunftsquelle ist zu verstehen, dass die betroffenen Wirtschaftsgüter eine eigenständige Erwerbsgrundlage bilden. Maßgeblich ist also die Frage, ob mit der Kryptowährung Einkünften erzielt werden.
> 
> Beim Lending werden jedoch in der Regel keine Einkünfte aus dem Wirtschaftsgut (der Kryptowährung), sondern aus dem Verleihgeschäft erzielt (als Ertrag aus der Forderung). Weil in diesen Fällen kein Missbrauch vorliegt, kann es bei der Haltefrist von einem Jahr bleiben. Auch das Bayrische Landesamt für Steuern hat bestätigt, dass die erhaltenen Zinsen nicht Ausfluss des „anderen Wirtschaftsgutes Fremdwährungsguthaben“, sondern vielmehr Ausfluss der eigentlichen Kapitalforderungen sind.

[Quelle](https://www.winheller.com/bankrecht-finanzrecht/bitcointrading/bitcoinundsteuer/besteuerung-lending.html)
[Wörtlich zitiert vom 14.02.2021]

Zusammenfassung in meinen Worten:
- Erhaltene Kryptowährung durch Coin Lending wird im Zeitpunkt des Zuflusses als Einkunft aus sonstigen Leistungen versteuert (Freigrenze 256 €).
- Der Verkauf ist nicht steuerbar.
- Coin Lending beeinflusst nicht die Haltefrist der verliehenen Coins.