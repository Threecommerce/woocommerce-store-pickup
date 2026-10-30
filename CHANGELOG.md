# Changelog

Tutte le modifiche rilevanti a questo plugin sono documentate in questo file.

Il formato è basato su [Keep a Changelog](https://keepachangelog.com/it/1.1.0/)
e questo progetto aderisce al [Semantic Versioning](https://semver.org/lang/it/).

## [1.0.1] - 2026-10-28

### Fixed
- Checkout a blocchi: l'ordine con ritiro veniva sempre rifiutato (`wo_sp_store_missing`) perché l'extension data
  `wo-store-pickup` della Store API non veniva registrata: `woocommerce_blocks_loaded` è già stato lanciato quando il
  plugin parte. Ora la registrazione avviene subito se l'hook è già passato, altrimenti all'hook.
- Checkout a blocchi: aggiunta la dipendenza `wc-blocks-data-store` allo script del selettore (avviso in console
  "wcBlocksData ... without proper dependency declaration").

### Changed
- Checkout a blocchi, vista mappa: sotto la mappa compare "Negozio scelto: <nome>" dopo il clic sul marker.
- README: senza Threecommerce Store Locator il plugin si attiva ma resta inerte e mostra un avviso (non "non si attiva").

## [1.0.0] - 2026-10-27

### Added
- Metodo di spedizione WooCommerce **Ritiro in negozio** (`wo_store_pickup`), da aggiungere alle zone di
  spedizione: titolo, costo (vuoto o 0 = gratuito), stato delle tasse e paesi ammessi. Non è disponibile se nessun
  negozio è abilitato al ritiro.
- Flag **Disponibile per il ritiro** sulla scheda negozio di Threecommerce Store Locator (filtro `wo_sl_store_fields`
  del locator) e colonna nell'elenco negozi.
- Scelta del negozio al checkout, da **elenco** o da **mappa** (OpenStreetMap o Google Maps, la stessa configurazione dello
  store locator), mostrata solo con il metodo di ritiro selezionato:
  - checkout classico (shortcode): riga della tabella di riepilogo ordine stampata dal server, con vista mappa;
  - checkout a blocchi: selettore nello slot del blocco Spedizione (`ExperimentalOrderShippingPackages`), scelta
    inviata con `extensionCartUpdate` e come extension data della richiesta di checkout (Store API).
- Validazione lato server in entrambi i flussi: l'ordine con il ritiro e senza un negozio valido non può essere effettuato.
- Il negozio scelto (id, nome, indirizzo, telefono) è salvato come meta dell'ordine (compatibile con HPOS) e mostrato
  nell'ordine in admin, nella pagina di conferma, nelle e-mail dell'ordine e in Il mio account.
- `pickup-map.js` (stessa struttura del modulo Magento `m2-store-pickup`), traduzione italiana, dichiarazione di
  compatibilità con HPOS e con i blocchi Carrello/Checkout.
- Porting per WooCommerce del modulo Magento `threecommerce/m2-store-pickup` 2.1.0.
