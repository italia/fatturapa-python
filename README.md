# FatturaPA-python
Tool for quick, command-line generation of simple e-Invoice compatible with the Italian-standard, [FatturaPA](https://www.fatturapa.gov.it). This is a [developers.italia.it](https://developers.italia.it/) Community Edition, version statically forked from [github.com/walter-arrighetti/](https://github.com/walter-arrighetti)[**pyFatturaPA**](https://github.com/walter-arrighetti/pyFatturaPA).
It is a typical, lazy sunday afternoon exercise, aimed at self-generating e-invoices to private companies as an individual freelance consultant.A rudimetary command-line generator of XML e-invoices to be later electronically signed or sealed. It generates a JSON database of clients (with VAT# and full invoicing information). More and more complex invoicing scenarios will be added in future releases.

***DISCLAIMER***: The author denies any responsibilities, either explicit or implied, on possible damages and liabilities derived or implied by the use of this software tool. In particular, no assumption of validity or compatibility on the software deliverables must be assumed. Also, the software is supplied *as is* (in GNU GPL terminology).

Due to the validity of such e-invoicing standard being limited to Italian finance, the README continues in Italian.

<img src="opt/pyFatturaPA_icon.png" />

### Descrizione
Questo tool viene inizialmente impiegato per costituire un database contenente un elenco essenziale di committenti (ove sono registrate le loro informazioni fiscali quali P.IVA, indirizzo PEC, C.F., ecc.). Il database, chiamato `pyFatturaPA.conf.json`, deve trovarsi nella medesima cartella del tool, così come si consiglia di eseguirlo da tale cartella.

Sempre mediante lo stesso (cfr. sezione **Sintassi**), si possono generare singole fatture elettroniche in formato XML che rispettano lo standard [*FatturaPA* 1.2.1](https://www.fatturapa.gov.it/export/fatturazione/it/normativa/f-2.htm). La sintassi del nome del file generato è `IT`*`numPartitaIVA`*`_`*`numFattura`*`.xml`, cioè combinando il numero di P.IVA emettente e l'identificativo univoco di quella fattura elettronica specifica.

Tali fatture elettroniche sono pronte per essere *firmate* (da parte del cedente/prestatore) ovvero *sigillate elettronicamente* (da parte dell'[Agenzia delle Entrate](https://www.agenziaentrate.gov.it)), per poi essere inviate al [*Sistema di Interscambio* dell'Agenzia delle Entrate](https://ivaservizi.agenziaentrate.gov.it/portale/) stessa e, da li, in conservazione sostitutiva.

### Sintassi
```
pyFatturaPA   consulenza | emetti | committente | inizializza
```
Il tool effettua quattro possibili operazioni:
 
 `emetti` genera una singola fattura con opzioni piuttosto complete; sono infatti supportate diverse tipologie di fattura/ritenuta/nota, esigibilità, aliquota, condizioni e modalità di pagamento, nonché causali, quantità e unità di misura per voci multiple nella fatturazione. Sono supportate fatture elettroniche verso paesi UE ed extra UE. L'eventuale IBAN ove pagare la fatturazione (in caso di pagamenti tramite bonifico) può essere preso automaticamente dalle informazioni del cedente/prestatore (nel database), immesso manualmente, ovvero omesso.
 
 `consulenza` è una versione specializzata del precedente; crea ancor più rapidamente una singola fattura, relativa ad una prestazione senza alcuna cessazione/trasferimento di beni, da parte di un professionista soggetto ad IVA (22%), alla cassa INPS (4%) e a ritenuta d'acconto (−20%). La generazione della fattura elettronica avviene inserendo solamente i **6** campi generici (*obbligatori* se in corsivo):
  * *sigla identificativa del committente* (3 caratteri, così come indicata nel database dei committenti/cessionari),
  * *numero identificativo progressivo della fattura*,
  * numero d'ordine del committente cui la fattura fa riferimento,
  * giorni ammessi per il pagamento dall'emissione,
  * codice IBAN cui intestare il pagamento (qualora non  compreso nelle informazioni del prestatore d'opera nel database),
  * causale complessiva della fattura;

più *almeno una* voce di fatturazione, ciascuna corrispondente a distinte afferenti la medesima fattura.

 `inizializza` inizializza il database  (`pyFatturaPA.conf.json`) creandone uno vuoto e inserendovi *una tantum* le sole informazioni del cedente/prestatore, dalle quali viene anche determinato se è soggetto a vati tipi di casse o ritenute.
 
 `committente` permette di aggiungere al database dei fornitori/committenti un'ulteriore voce, che sarà poi indicizzata mediante codice a 3 cifre alfanumeriche. Non è attualmente possibile rimuovere un cessionario/committente.

***DISCLAIMER***: L'autore nega ogni responsabilità, diretta o indiretta, circa l'uso del software e dei suoi derivati. In particolare non viene fatta alcuna presunzione di validità e conformità delle evidenze informatiche prodotte con gli standard tecnici di riferimento. Inoltre, il software è fornito *così com'è*, secondo i termini della licenza utilizzata.
