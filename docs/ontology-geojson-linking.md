# Ontology and GeoJSON Linking

This document explains how the OWL/JSON-LD ontology is linked to the GeoJSON spatial data in SacredGeoKB.

## Linking Rule

- Ontology concepts use `associated_zone_ids`, `outside_zone_ids`, or `source_zone_id` to reference spatial zone identifiers.
- GeoJSON features use the same identifier in `feature.id` and `feature.properties.id`.
- A concept is spatially linked when one of its zone references equals a GeoJSON feature id.
- GeoJSON coordinates follow the standard `[longitude, latitude]` order.

## Files

- `ontology/hajj-ontology.owl`: OWL/RDF export of the ontology.
- `ontology/hajj-ontology.jsonld`: source ontology in JSON-LD style.
- `geojson/spatial-zones.geojson`: normalized FeatureCollection for all spatial zones.
- `geojson/openstreetmap/*.geojson`: original OpenStreetMap GeoJSON source files used to build selected zones.

## Concept to GeoJSON Mapping

| Ontology id | Type | Title | Zone ids | Matched GeoJSON features |
| --- | --- | --- | --- | --- |
| `AlIhram` | `Ritual` | Al-Ihram | `dhul_hulayfah_miqat`, `juhfah_miqat`, `qarn_al_manazil_miqat`, `yalamlam_miqat`, `dhat_irq_miqat`, `makkah_haram_boundary`, `alharam` | `makkah_haram_boundary`, `alharam` |
| `Tawaf` | `Ritual` | Tawaf | `kaaba`, `tawaf`, `alharam` | `kaaba`, `alharam` |
| `TawafAlIfadhah` | `Ritual` | Tawaf al-Ifadhah | `kaaba`, `tawaf`, `alharam` | `kaaba`, `alharam` |
| `TawafAlWadaa` | `Ritual` | Tawaf al-Wadaa | `kaaba`, `tawaf`, `alharam`, `makkah_city` | `kaaba`, `alharam` |
| `Sai` | `Ritual` | Sa'i | `safa`, `marwah`, `sai` | `safa`, `marwah`, `sai` |
| `StandingInArafat` | `Ritual` | Standing in Arafat | `arafat`, `jabal_al_rahmah`, `namirah_mosque`, `jabal_namirah`, `mashair_train_arafat_3_station` | `arafat`, `jabal_al_rahmah`, `namirah_mosque`, `jabal_namirah`, `mashair_train_arafat_3_station` |
| `SpendingNightInMuzdalifah` | `Ritual` | Spending the night in Muzdalifah | `muzdalifah`, `mashair_train_muzdalifah_station` | `muzdalifah`, `mashair_train_muzdalifah_station` |
| `SpendingNightInMina` | `Ritual` | Spending the night in Mina | `mina` | `mina` |
| `Rami` | `Ritual` | Stoning of the Devil / Rami | `jamarat_al_aqaba`, `jamarat_al_wusta`, `jamarat_al_sughra`, `mina` | `jamarat_al_aqaba`, `jamarat_al_sughra`, `mina` |
| `DayOfTarwiyah` | `ReligiousOccasion` | Day of Tarwiyah | `mina` | `mina` |
| `DayOfArafat` | `ReligiousOccasion` | Day of Arafat | `arafat`, `jabal_al_rahmah`, `namirah_mosque`, `jabal_namirah`, `mashair_train_arafat_3_station` | `arafat`, `jabal_al_rahmah`, `namirah_mosque`, `jabal_namirah`, `mashair_train_arafat_3_station` |
| `MuzdalifahNight` | `ReligiousOccasion` | Night at Muzdalifah | `muzdalifah`, `mashair_train_muzdalifah_station` | `muzdalifah`, `mashair_train_muzdalifah_station` |
| `EidAlAdha` | `ReligiousOccasion` | Eid al-Adha | `mina`, `jamarat_al_aqaba` | `mina`, `jamarat_al_aqaba` |
| `FirstTashreeqNight` | `ReligiousOccasion` | First Tashreeq Night | `mina` | `mina` |
| `DaysOfTashreeq` | `ReligiousOccasion` | Days of Tashreeq | `mina`, `jamarat_al_aqaba`, `jamarat_al_sughra` | `mina`, `jamarat_al_aqaba`, `jamarat_al_sughra` |
| `MakkahHaramBoundaryPlace` | `SacredPlace` | Makkah Haram Boundary | `makkah_haram_boundary` | `makkah_haram_boundary` |
| `AlHaramPlace` | `SacredPlace` | Al-Haram | `alharam` | `alharam` |
| `KaabaPlace` | `SacredPlace` | The Kaaba | `kaaba` | `kaaba` |
| `ProphetMosquePlace` | `SacredPlace` | Prophet's Mosque | `prophetMosque` | `prophetMosque` |
| `KaabaAndMataf` | `SacredPlace` | Kaaba and Mataf | `kaaba`, `tawaf` | `kaaba` |
| `SafaMarwa` | `SacredPlace` | Safa and Marwa | `safa`, `marwah`, `sai` | `safa`, `marwah`, `sai` |
| `ArafatPlace` | `HajjPlace` | Arafat | `arafat`, `jabal_al_rahmah`, `namirah_mosque`, `jabal_namirah` | `arafat`, `jabal_al_rahmah`, `namirah_mosque`, `jabal_namirah` |
| `MuzdalifahPlace` | `HajjPlace` | Muzdalifah | `muzdalifah`, `mashair_train_muzdalifah_station` | `muzdalifah`, `mashair_train_muzdalifah_station` |
| `MinaPlace` | `HajjPlace` | Mina | `mina`, `jamarat_al_aqaba`, `jamarat_al_sughra` | `mina`, `jamarat_al_aqaba`, `jamarat_al_sughra` |
| `JamaratPlace` | `HajjPlace` | Jamarat | `jamarat_al_aqaba`, `jamarat_al_wusta`, `jamarat_al_sughra` | `jamarat_al_aqaba`, `jamarat_al_sughra` |
| `MiqatPlace` | `HajjPlace` | Miqat | `dhul_hulayfah_miqat`, `juhfah_miqat`, `qarn_al_manazil_miqat`, `yalamlam_miqat`, `dhat_irq_miqat` | Not in `spatial-zones.geojson` |
| `ZoneSemantic_makkah_haram_boundary` | `SpatialZoneSemantic` | Makkah Haram Boundary | `makkah_haram_boundary` | `makkah_haram_boundary` |
| `ZoneSemantic_bab_al_salam_haram` | `SpatialZoneSemantic` | Bab Al-Salam - Al-Haram | `bab_al_salam_haram` | `bab_al_salam_haram` |
| `ZoneSemantic_bab_king_abdulaziz_haram` | `SpatialZoneSemantic` | King Abdulaziz Gate - Al-Haram | `bab_king_abdulaziz_haram` | `bab_king_abdulaziz_haram` |
| `ZoneSemantic_bab_al_umrah_haram` | `SpatialZoneSemantic` | Umrah Gate - Al-Haram | `bab_al_umrah_haram` | `bab_al_umrah_haram` |
| `ZoneSemantic_alharam` | `SpatialZoneSemantic` | Al-Haram | `alharam` | `alharam` |
| `ZoneSemantic_kaaba` | `SpatialZoneSemantic` | The Kaaba | `kaaba` | `kaaba` |
| `ZoneSemantic_tawaf` | `SpatialZoneSemantic` | Tawaf Area | `tawaf` | Not in `spatial-zones.geojson` |
| `ZoneSemantic_safa` | `SpatialZoneSemantic` | Sa'i Path | `safa` | `safa` |
| `ZoneSemantic_marwah` | `SpatialZoneSemantic` | Al-Marwah | `marwah` | `marwah` |
| `ZoneSemantic_mina` | `SpatialZoneSemantic` | Mina Camp | `mina` | `mina` |
| `ZoneSemantic_jamarat_al_aqaba` | `SpatialZoneSemantic` | Jamarat Al-Aqaba | `jamarat_al_aqaba` | `jamarat_al_aqaba` |
| `ZoneSemantic_jamarat_al_sughra` | `SpatialZoneSemantic` | Jamarat Al-Sughra | `jamarat_al_sughra` | `jamarat_al_sughra` |
| `ZoneSemantic_arafat` | `SpatialZoneSemantic` | Arafat Plain | `arafat` | `arafat` |
| `ZoneSemantic_mashair_train_arafat_3_station` | `SpatialZoneSemantic` | Al Mashaaer Train - Arafat 3 Station | `mashair_train_arafat_3_station` | `mashair_train_arafat_3_station` |
| `ZoneSemantic_pedestrian_route_muzdalifah_arafat` | `SpatialZoneSemantic` | Pedestrian Route between Muzdalifah and Arafat | `pedestrian_route_muzdalifah_arafat` | `pedestrian_route_muzdalifah_arafat` |
| `ZoneSemantic_jabal_namirah` | `SpatialZoneSemantic` | Jabal Namirah | `jabal_namirah` | `jabal_namirah` |
| `ZoneSemantic_namirah_mosque` | `SpatialZoneSemantic` | Namirah Mosque | `namirah_mosque` | `namirah_mosque` |
| `ZoneSemantic_jabal_al_rahmah` | `SpatialZoneSemantic` | Jabal al-Rahmah | `jabal_al_rahmah` | `jabal_al_rahmah` |
| `ZoneSemantic_muzdalifah` | `SpatialZoneSemantic` | Muzdalifah | `muzdalifah` | `muzdalifah` |
| `ZoneSemantic_mashair_train_muzdalifah_station` | `SpatialZoneSemantic` | Al Mashaaer Train - Muzdalifah Station | `mashair_train_muzdalifah_station` | `mashair_train_muzdalifah_station` |
| `ZoneSemantic_prophetMosque` | `SpatialZoneSemantic` | Prophet's Mosque | `prophetMosque` | `prophetMosque` |
| `ZoneSemantic_bab_quba_prophet_mosque` | `SpatialZoneSemantic` | Quba Gate - Prophet Mosque | `bab_quba_prophet_mosque` | `bab_quba_prophet_mosque` |
| `ZoneSemantic_bab_bilal_prophet_mosque` | `SpatialZoneSemantic` | Bilal Gate - Prophet Mosque | `bab_bilal_prophet_mosque` | `bab_bilal_prophet_mosque` |
| `ZoneSemantic_bab_king_saud_prophet_mosque` | `SpatialZoneSemantic` | King Saud Gate - Prophet Mosque | `bab_king_saud_prophet_mosque` | `bab_king_saud_prophet_mosque` |
| `ZoneSemantic_bab_al_aqiq_prophet_mosque` | `SpatialZoneSemantic` | Al-Aqiq Gate - Prophet Mosque | `bab_al_aqiq_prophet_mosque` | `bab_al_aqiq_prophet_mosque` |
| `ZoneSemantic_bab_omar_ibn_al_khattab_prophet_mosque` | `SpatialZoneSemantic` | Omar ibn Al-Khattab Gate - Prophet Mosque | `bab_omar_ibn_al_khattab_prophet_mosque` | `bab_omar_ibn_al_khattab_prophet_mosque` |
| `ZoneSemantic_bab_badr_prophet_mosque` | `SpatialZoneSemantic` | Badr Gate - Prophet Mosque | `bab_badr_prophet_mosque` | `bab_badr_prophet_mosque` |
| `ZoneSemantic_bab_king_fahd_prophet_mosque` | `SpatialZoneSemantic` | King Fahd Gate - Prophet Mosque | `bab_king_fahd_prophet_mosque` | `bab_king_fahd_prophet_mosque` |
| `ZoneSemantic_bab_uhud_prophet_mosque` | `SpatialZoneSemantic` | Uhud Gate - Prophet Mosque | `bab_uhud_prophet_mosque` | `bab_uhud_prophet_mosque` |
| `ZoneSemantic_bab_uthman_ibn_affan_prophet_mosque` | `SpatialZoneSemantic` | Uthman ibn Affan Gate - Prophet Mosque | `bab_uthman_ibn_affan_prophet_mosque` | `bab_uthman_ibn_affan_prophet_mosque` |
| `ZoneSemantic_bab_ali_ibn_abi_talib_prophet_mosque` | `SpatialZoneSemantic` | Ali ibn Abi Talib Gate - Prophet Mosque | `bab_ali_ibn_abi_talib_prophet_mosque` | `bab_ali_ibn_abi_talib_prophet_mosque` |
| `ZoneSemantic_bab_abu_dharr_al_ghifari_prophet_mosque` | `SpatialZoneSemantic` | Abu Dharr Al-Ghifari Gate - Prophet Mosque | `bab_abu_dharr_al_ghifari_prophet_mosque` | `bab_abu_dharr_al_ghifari_prophet_mosque` |
| `ZoneSemantic_bab_king_abdulaziz_prophet_mosque` | `SpatialZoneSemantic` | King Abdulaziz Gate - Prophet Mosque | `bab_king_abdulaziz_prophet_mosque` | `bab_king_abdulaziz_prophet_mosque` |
| `ZoneSemantic_bab_makkah_prophet_mosque` | `SpatialZoneSemantic` | Makkah Gate - Prophet Mosque | `bab_makkah_prophet_mosque` | `bab_makkah_prophet_mosque` |
| `ZoneSemantic_bab_al_baqia_prophet_mosque` | `SpatialZoneSemantic` | Al-Baqi Gate - Prophet Mosque | `bab_al_baqia_prophet_mosque` | `bab_al_baqia_prophet_mosque` |
| `ZoneSemantic_bab_jebril_prophet_mosque` | `SpatialZoneSemantic` | Jibril Gate - Prophet Mosque | `bab_jebril_prophet_mosque` | `bab_jebril_prophet_mosque` |
| `ZoneSemantic_bab_al_nisaa_prophet_mosque` | `SpatialZoneSemantic` | Al-Nisaa Gate - Prophet Mosque | `bab_al_nisaa_prophet_mosque` | `bab_al_nisaa_prophet_mosque` |
| `ZoneSemantic_bab_al_rahmah_prophet_mosque` | `SpatialZoneSemantic` | Al-Rahmah Gate - Prophet Mosque | `bab_al_rahmah_prophet_mosque` | `bab_al_rahmah_prophet_mosque` |
| `ZoneSemantic_miqat_dhu_hulayfah` | `SpatialZoneSemantic` | Miqat Dhu al-Hulayfah | `miqat_dhu_hulayfah` | `miqat_dhu_hulayfah` |
| `ZoneSemantic_miqat_qarn_al_manazil` | `SpatialZoneSemantic` | Miqat Qarn al-Manazil | `miqat_qarn_al_manazil` | `miqat_qarn_al_manazil` |
| `ZoneSemantic_miqat_yalamlam` | `SpatialZoneSemantic` | Miqat Yalamlam | `miqat_yalamlam` | `miqat_yalamlam` |
| `ZoneSemantic_miqat_dhat_irq` | `SpatialZoneSemantic` | Miqat Dhat Irq | `miqat_dhat_irq` | `miqat_dhat_irq` |
| `ZoneSemantic_miqat_al_juhfah` | `SpatialZoneSemantic` | Miqat Al-Juhfah / Rabigh | `miqat_al_juhfah` | `miqat_al_juhfah` |
| `ZoneSemantic_sai` | `SpatialZoneSemantic` | Sa'i / Al Masa'a Safa - Marwa | `sai` | `sai` |
| `ZoneSemantic_al_hijr` | `SpatialZoneSemantic` | Hijr Ismail (Al-Hijr / Hateem) | `al_hijr` | `al_hijr` |
| `AlHijrPlace` | `SacredPlace` | Hijr Ismail (Al-Hijr / Hateem) | `al_hijr` | `al_hijr` |
