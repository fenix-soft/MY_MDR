# Come utilizzare il comando gzip in Linux (guida rapida)

***gzip*** è una delle utility di compressione dati più usata, sopratutto per la sua retro-compatibilità per lo scambio dati in vecchi sistemi operativi, server e reti http, sistemi embedded dove richiede poche risorse, sia in cpu che di memoria. 
In ambiti dove sono richiesti tempi di compressione e decompressione rapidi e facilmente implementabili. Esistono chip hardware che comprimono o decomprimono in tale formato (gzip, deflate). Il programma è utilizzato come libreria in molteplici software, git, browser-web, gimp, ecc.

Il progetto, nasce nel 1992, ad opera dei programmatori Jean-Loup Gailly e Mark Adler, che si erano prefissati il compito di sviluppare un’alternativa convincente a **compress**, programma scritto per Unix, che utilizava allora un algoritmo coperto da brevetto (LZW).

Il programma gzip, che è la forma abbreviata di “**GNU zip**”, si basa sul algoritmo **Deflate**, (pkzip, zip) utilizzabile liberamente e che consiste in una variazione del processo di compressione dei dati **LZ77** (Lempel-Ziv 77), e sulla codifica di Huffman. Proprio con l’aiuto di queste tecniche gzip scansiona i file in cerca di stringhe di dati ricorrenti. Nel caso in cui il programma incontri determinate sequenze ricorrenti, queste vengono sostituite attraverso un dizionario a finestra scorrevole, sulla prima stringa che compare, dove la lunghezza di una tale sequenza è solitamente limitata a 32 Kbyte, per poi essere processate con la codifica di Huffman. Se una sequenza non si presenta nei 32 kbyte precedenti, allora il file verrà salvato senza compressione dati. Il procedimento è limitato ai singoli file, perciò per cartelle di file è necessario un programma di archiviazione esterno al fine di creare dei cosiddetti **archivi compressi**, con estensioni .tar.gz o .tgz.

Il programma gzip è stato originariamente sviluppato per la piattaforma **GNU Linux**, ma oggi è utilizzabile su quasi ogni piattaforma, fin quanto la licenza GPL scelta per il progetto venga rispettata. Ad esempio sui sistemi Linux, questo strumento per la compressione dei dati è solitamente installato automaticamente o in alternativa è contenuto nel sistema di gestione dei pacchetti, pronto per essere installato.

Oltre alle varie edizioni per i sistemi operativi più datati, esistono anche versioni per macOS e Windows, scaricabili sulla [pagina ufficiale di gzip](https://www.gzip.org/).
 Inoltre la compressione di gzip è utilizzata da anni da programmi per la gestione dei server web come ad esempio Apache, anche se questa funzione non viene sempre utilizzata, e dai browser moderni, che sono in grado di interpretare i file compressi e di decomprimerli durante il rende-ring dei siti web.

Il programma gzip mostra il meglio di sé nell'ambito dello sviluppo web: una volta attivato il processo, il server web inizia automaticamente la compressione degli elementi caricati nello spazio web così come degli elementi dinamici del sito web. In questo modo il tempo di caricamento del sito web sarà considerevolmente inferiore per il visitatore. Dovendo quindi gli utenti caricare solamente i pacchetti dati compressi, le stesse pagine web sono notevolmente più rapide da ricostruire. 

*In questa mini guida impareremo assieme ad utilizzare questo pratico strumento.*

---

## Usare il comando gzip su terminale Linux

Per utilizzare il comando **gzip**, dovrai seguire la sintassi indicata:


    gzip [opzioni] file


L’immissione di opzioni non è in alcun modo obbligatoria. Lasciando il campo vuoto, gzip farà riferimento alle impostazioni standard, comprimendo il file di partenza con un nuovo file con estensione gz, e rimuovendo il file d'origine.


### Comprimere un file utilizzando il comando gzip

Per comprimere un file utilizzando il comando gzip, tutto ciò che devi fare è aggiungere il percorso del file al comando gzip:

    gzip filename

Ad esempio, qui, ho compresso un file di testo:

    gzip esempio.txt

dopo la compressione e l'eliminazione automatica del file origine (esempio.txt) avremo un file chiamato:

    esempio.txt.gz

se vogliamo mantenere il file originale (vogliamo prevenire la cancellazione automatica utilizziamo l'opzione -k) in questo modo:

    gzip -k esempio.txt


se diamo un **ls** per visualizzare il contenuto della directory cartella corrente avremo entrambi i file:

    esempio.txt
    esempio.txt.gz

Per decomprimere pacchetti compressi in precedenza, si può fare affidamento sia sul programma **gunzip** sia sul corrispettivo comando di **gzip -d**

    gzip -d esempio.txt.gz

oppure se vogliamo mantenere entrambi i file:

    gzip -k -d esempio.txt

La seguente tabella fornisce i comandi gzip più importanti:


|Opzione|Descrizione|
|-------|-----------|
|**-1 … -9**|Definisce il grado di compressione (1-9), dove il valore 1 corrisponde al tipo di compressione più basso e veloce, mentre il valore 9 equivale a quello migliore ma che richiede un maggior tempo; il valore standard preimpostato è 5|
|**-r**|Ricerca ricorsivamente la cartella (incluse tutte le sottocartelle) e comprime o decomprime tutti i file contenuti al suo interno|
|**-f**|Forza la compressione gzip e sovrascrive, in caso sia necessario, i file già presenti con lo stesso nome|
|**-d**|Decomprime i file selezionati nella cartella attuale|
|**-k**|Impedisce la cancellazione del file originale|
|**-l**|Mostra le informazioni dei file, come ad esempio il grado di compressione|
|**-c**|Crea un file compresso per uno standard output, di solito lo schermo di un PC, connesso alla riga di comando|
|**-q**|Disattiva completamente le comunicazioni da parte del programma gzip|
|**-t**|Testa l’integrità del file compresso|
|**-h**|Elenca tutte le opzioni disponibili |

per maggiori informazioni consultare il manuale del programma con il comando:

    man gzip



## Come comprimere con gzip una directory in Linux

Come accennato precedentemente **gzip** opera unicamente su un singolo file per volta, quindi in parole spicce è impossibilitato a comprimere intere directory di file in un unico file compresso, per fare ciò si usa prima archiviare con **tar** la directory/cartella da comprimere, per poi comprimerla in un secondo momento con gzip.

    gzip archivio.tar

avremo un file chiamato:

    archivio.tar.gz

questo approccio potrebbe risultare scomodo (comandi archivio tar + comandi gizp), perché effettivamente andremo a scrivere una miriade di comandi, fortunatamente è possibile fare questa operazione direttamente con un unico comando tar simile a questo:

    tar -zcvf nome_archivio cartella_da_comprimere

le opzioni del comando **tar** utilizzato in precedenza hanno il seguente significato:

    z   dice a tar che deve usare gzip per comprimere il file
    c   dice a tar di creare archivio di file non compresso
    v   modalità dettagliata, mostra quali file vengono elaborati
    f   l'output file 
    x   estrae i file dall'archivio
    

vediamo un esempio, supponiamo che ho una cartella chiamata "documenti" contenente file vari, vorrei comprimerla con gz in un archivio compresso tar.gz chiamato archivio_documenti:

    tar -zcvf archivio_documenti.tar.gz documenti

per estrarlo:

    tar -zxvf archivio_documenti.tar.gz

se il file presenta estensione "tar.gz" **tar** è in grado di riconoscerlo come "archivio compresso gzip" e si può omettere il parametro **'z'** in fase di estrazione:

    tar -xvf archivio_documenti.tar.gz

con GNU TAR è anche possibile passare parametri opzionali al "compressore", supponiamo ad esempio di voler comprimere e archiviare la solita cartella documenti, questa volta contenente ad esempio solo file di testo semplice (hanno un alto rapporto di compressione) e di voler utilizzare un grado di compressione di gzip di tipo -9 "migliore" a discapito del tempo, avremo un comando simile a questo:

    tar -c -I 'gzip -9' -vf archivio_documenti.tar.gz documenti

le opzioni del comando **tar** utilizzato in precedenza hanno il seguente significato:


    -c   dice a tar di creare archivio di file non compresso
    -I   indica il programma di compressione e i parametri da usare
    -v   modalità dettagliata, mostra quali file vengono elaborati
    -f   l'output file 

per ulteriori combinazioni di comandi fare riferimento al manuale di GNU TAR.

    man tar

