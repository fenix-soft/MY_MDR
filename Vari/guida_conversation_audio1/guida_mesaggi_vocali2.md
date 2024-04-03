# Guida: come ottimizzare i messaggi vocali in conversation per android (Parte 2)

Come accennato nella parte prima della guida, non tutti i dispositivi android riescono  ad interfacciare la codifica OPUS (encoder di sistema) con l'applicativo RecordYou, tralasciando i tecnicismi del problema,  andreamo ad utilizzare la codifica **AAC** incapsulata in un contenitore **M4A** .

Il motivo per l'utilizzo di M4A e non di un file AAC grezzo, risiede nel fatto che, "AAC file grezzo" non è riconosciuto dal lettore multimediale audio integrato in conversation (in sostanza lo legge come un file allegato generico, e non carica il player), che supporta solo come contenitori audio (ogg,oga,m4a).



