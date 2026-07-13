# Hajj Rituals Ontology for Ouns

This ontology models pilgrimage rituals, religious occasions, places, and contextual inference rules used by Ouns.

## Metadata

Each ontology node includes metadata fields: `creator`, `title`, `data_identifier`, `publisher`, `publication_date`, `summary`, and `keywords`.

```text
creator: Ghader Kurdi
publisher: Ghader Kurdi
publication_date: 2026-07-11
```

## Core Classes

- `Journey`: A structured pilgrimage or visit path.
- `Ritual`: A worship action or ritual state in the pilgrimage journey.
- `ReligiousOccasion`: A religiously significant time window during Hajj.
- `SacredPlace`: A sacred place associated with a ritual.
- `HajjPlace`: A Hajj-related place or site.
- `QuranVerse`: A Quran verse referenced by ontology concepts.
- `IslamPillar`: One of the five foundational pillars of Islam.
- `RelationshipProperty`: A semantic relation used to connect ontology entities.

## Core Relations

| Relation | Connects From | Connects To | Meaning |
| --- | --- | --- | --- |
| `part_of` | `ReligiousOccasion`, `SacredPlace`, or `HajjPlace` | `Journey` or broader ontology entity | Indicates that a non-ritual entity belongs to a larger journey or concept. |
| `ritual_of` | `Ritual` | `Journey` | Connects a ritual to the pilgrimage journey in which it is performed. |
| `has_ritual` | `Journey` | `Ritual` | Connects a pilgrimage journey to the rituals included in it. |
| `has_sub_ritual` | `Ritual` | `Ritual` | Connects a general ritual to a more specific ritual type. |
| `sub_ritual_of` | `Ritual` | `Ritual` | Connects a specific ritual type to its broader ritual category. |
| `has_occasion` | `Journey` | `ReligiousOccasion` | Connects a journey to a religious occasion that occurs within it. |
| `precedes` | `Ritual` or `ReligiousOccasion` | `Ritual` or `ReligiousOccasion` | Indicates that one entity usually occurs before another. |
| `follows` | `Ritual` or `ReligiousOccasion` | `Ritual` or `ReligiousOccasion` | Indicates that one entity usually occurs after another. |
| `associated_place` | `Ritual` or `ReligiousOccasion` | `SacredPlace` or `HajjPlace` | Links a ritual or occasion to the place where it is performed or primarily associated. |
| `associated_occasion` | `Ritual` | `ReligiousOccasion` | Links a ritual to the religious occasion or time window in which it is primarily performed. |
| `located_in_city` | `SacredPlace` or `HajjPlace` | `HajjPlace` city node | Links a place to the city where it is located. |
| `contains_place` | `HajjPlace` city node | `SacredPlace` or `HajjPlace` | Links a city to the sacred or Hajj places it contains. |
| `gate_of` | `SpatialZoneSemantic` gate | `SacredPlace` | Links a door/gate spatial zone to the mosque or sacred place it belongs to. |
| `has_gate` | `SacredPlace` | `SpatialZoneSemantic` gate | Links a mosque or sacred place to its door/gate spatial zones. |
| `mentioned_in_quran` | Ontology concept | `QuranVerse` | Links a concept to a Quran verse that mentions or establishes it. |
| `mentions_concept` | `QuranVerse` | Ontology concept | Links a Quran verse to the ontology concepts it mentions. |
| `islam_pillar` | Ontology concept | `IslamPillar` | Links a concept such as Hajj journey to the corresponding pillar of Islam. |
| `represented_by` | `IslamPillar` | Ontology concept | Links a pillar concept to the ontology node that operationalizes it. |
| `performed_in_city` | `Journey` or `Ritual` | `HajjPlace` city node | Links a journey or ritual concept to the city where it is primarily performed. |
| `outside_zone_ids` | `Ritual` or rule node | `Spatial zone id` | Indicates zones that the ritual location is outside of; this is a spatial constraint, not an associated place. |

## Five Pillars of Islam

The ontology models the five pillars of Islam as `IslamPillar` concepts. Hajj is explicitly modeled as the fifth pillar and linked to the Hajj journey used by Ouns.

```text
ShahadaPillar: 1 - الشهادتان
SalahPillar: 2 - الصلاة
ZakatPillar: 3 - الزكاة
SawmPillar: 4 - صوم رمضان
HajjPillar: 5 - الحج: الركن الخامس من أركان الإسلام
```

Relations:

```text
HajjPillar represented_by HajjJourney
HajjPillar performed_in_city MakkahCity
HajjJourney islam_pillar HajjPillar
HajjJourney performed_in_city MakkahCity
```

## Main Rituals

### Al Ihram (The State of Consecration)

Al Ihram represents the state of consecration entered before Hajj or Umrah rituals. In Ouns, it can be inferred when the user is performing Hajj or Umrah and is inside or near a Miqat geofence.

In the ontology sequence, Al-Ihram precedes all subsequent Hajj and Umrah rituals, including Tawaf, Sa'i, Standing in Arafat, Rami, spending the night in Mina, and Hajj-specific Tawaf types.

The `associated_zone_ids` for Al-Ihram refer to Miqat geofences only. `makkah_haram_boundary` and `alharam` are not associated zones for Al-Ihram; they are modeled as outside/reference zones because the standard Miqat locations are outside the Makkah Haram boundary and outside Al-Haram.

Alternative labels:

```text
The State of Consecration
State of Consecration
Ihram
```

For Hajj, an additional Makkah-specific rule is modeled: if the pilgrim is already in Makkah, has completed Umrah and exited Ihram, or is a Makkah resident intending Hajj, the Day of Tarwiyah (8 Dhu al-Hijjah) is treated as the preferred context for entering Ihram for Hajj from Makkah. If the pilgrim delays Ihram until the ninth day of Dhu al-Hijjah, this remains permissible and should not be inferred as an error state.

Context state:

```text
ihram_preparation_state
hajj_ihram_from_makkah_state
```

Expected need:

```text
Ihram Preparation + Guidance
```

### Tawaf

Tawaf represents circumambulation around the Kaaba. In Ouns, it is associated with the Kaaba, Mataf, and Al-Haram zones. It can be inferred when the spatial engine detects circular movement around the Kaaba reference point.

Tawaf consists of seven complete circuits around the Kaaba. Each complete circuit counts as one Tawaf round.

Context state:

```text
ritual_performance_state
```

Expected need:

```text
Ritual Performance + Spiritual Focus
```

### Sa'i

Sa'i represents movement between Safa and Marwa. In Ouns, it can be inferred when the user is inside or near Safa, Marwa, or the Sa'i path and the spatial engine detects directional movement along the Safa-Marwa axis.

Sa'i consists of seven one-way traversals between Safa and Marwa. It starts at Safa and ends at Marwah on the seventh traversal.

Context state:

```text
ritual_performance_state
```

Expected need:

```text
Ritual Performance + Guidance
```

### Hair Shaving or Trimming

Hair shaving or trimming represents the ritual act of shaving the head or shortening the hair to complete the required release from Ihram. In Umrah, it follows Sa'i. In Hajj, it commonly follows Rami on Eid al-Adha.

Arabic label:

```text
حلق الشعر أو تقصيره
```

Context state:

```text
hair_shaving_state
```

Expected need:

```text
Completion + Exit Ihram Guidance
```

### Standing in Arafat

Standing in Arafat represents the Hajj ritual of being present in Arafat on the ninth day of the Islamic month of Dhu al-Hijjah and remaining there until sunset. It is modeled as a ritual, while Day of Arafat is modeled as the religious occasion.

In Ouns, this state can be inferred when the journey type is Hajj, the Hijri date is the ninth day of Dhu al-Hijjah, the time is before or at sunset, and the user is inside or near Arafat-related geofences such as Arafat, Jabal al-Rahmah, or Masjid Namirah.

Arabic rule:

```text
يبقى الحاج في عرفة إلى غروب الشمس، ثم يبدأ الانتقال إلى مزدلفة بعد الغروب.
```

Context state:

```text
standing_in_arafat_state
```

Expected need:

```text
Spiritual Reflection + Reassurance
```

### Stoning of the Devil / Rami

Rami represents the Hajj ritual of stoning the Jamarat. It takes place at the three stone pillars in Mina: Jamarat al-Sughra, Jamarat al-Wusta, and Jamarat al-Aqaba.

In Ouns, this ritual can be inferred when the journey type is Hajj, the user is inside or near Mina or Jamarat-related geofences, and the date falls within the relevant Hajj days, especially Eid al-Adha and the Days of Tashreeq.

Context state:

```text
rami_performance_state
```

Expected need:

```text
Ritual Guidance + Crowd Awareness
```

Implementation note:

```text
The ontology includes the three Jamarat conceptually. The current spatial dataset contains Jamarat al-Aqaba and Jamarat al-Sughra; Jamarat al-Wusta should be linked once its geofence is added.
```

### Spending the Night in Mina

Spending the night in Mina represents the ritual state of remaining in Mina overnight during the Hajj sequence. In this ontology, it is explicitly linked to the First Tashreeq Night, which is modeled as a religious occasion associated with the tenth day of Dhu al-Hijjah.

In Ouns, this state can be inferred when the journey type is Hajj, the Hijri date is the tenth day of Dhu al-Hijjah, the time window is night, and the user remains inside or near the Mina geofence with stationary or very limited movement.

Context state:

```text
mina_overnight_state
```

Expected need:

```text
Rest + Ritual Reassurance
```

### Spending the Night in Muzdalifah

Spending the night in Muzdalifah represents the ritual state of remaining in Muzdalifah after departing Arafat and before proceeding to Mina. Its time begins after sunset on the Day of Arafat and continues through the night before the tenth day of Dhu al-Hijjah. It is linked to `MuzdalifahNight`, the night after the Day of Arafat and before Eid al-Adha / Day of Nahr.

In Ouns, this state can be inferred when the journey type is Hajj, the user is inside or near Muzdalifah-related geofences, and the time window is after sunset on the ninth day of Dhu al-Hijjah until before dawn of the tenth day.

Arabic rule:

```text
يبدأ وقت الوقوف بمزدلفة من بعد غروب شمس يوم عرفة.
```

Context state:

```text
muzdalifah_overnight_state
```

Expected need:

```text
Rest + Ritual Reassurance
```

## Religious Occasions

### Day of Tarwiyah

The Day of Tarwiyah is modeled as the eighth day of Dhu al-Hijjah. It is associated with preparation for Hajj movement and presence in Mina before the Day of Arafat.

It also supports the Makkah-specific Ihram case: a pilgrim who is in Makkah, has completed Umrah and exited Ihram, or is a Makkah resident intending Hajj may enter Ihram for Hajj on this day. Delaying Ihram until the ninth day is represented as permissible rather than invalid.

Context state:

```text
tarwiyah_day_state
```

Expected need:

```text
Preparation + Guidance
```

### Day of Arafat

The Day of Arafat is modeled as the ninth day of Dhu al-Hijjah and is associated with Arafat-related zones such as Arafat, Jabal al-Rahmah, and Masjid Namirah. It represents the time occasion, whereas Standing in Arafat represents the ritual act performed within that occasion.

Alternative labels:

```text
Day of Hajj
Yawm Arafah
يوم الحج
```

Disambiguation note: Day of Arafat is not modeled as `Day of the Greater Hajj` in this ontology. `Day of the Greater Hajj / Yawm al-Hajj al-Akbar` is modeled under Eid al-Adha / Day of Nahr on the tenth day of Dhu al-Hijjah, so the contextual engine does not confuse the 9th-day Arafat rule with the 10th-day Mina/Jamarat rule.

Context state:

```text
arafat_occasion_state
```

Expected need:

```text
Spiritual Reflection + Reassurance
```

### Eid al-Adha

Eid al-Adha is modeled as the tenth day of Dhu al-Hijjah. In the Hajj context, it is associated with Mina and Jamarat-related movement.

Alternative labels:

```text
Day of Nahr
Day of Sacrifice
Day of the Greater Hajj
Yawm al-Hajj al-Akbar
يوم النحر
يوم الحج الأكبر
```

Context state:

```text
eid_al_adha_state
```

Expected need:

```text
Ritual Guidance + Hospitality
```

### First Tashreeq Night

The First Tashreeq Night is modeled as the night associated with the tenth day of Dhu al-Hijjah. It is associated with Mina and with the ritual state of spending the night in Mina.

Context state:

```text
first_tashreeq_night_state
```

Expected need:

```text
Rest + Ritual Reassurance
```

### Muzdalifah Night

Muzdalifah Night is modeled as the night spent in Muzdalifah beginning after sunset on the Day of Arafat and before proceeding to Mina on the tenth day.

Arabic definition:

```text
تبدأ ليلة المبيت بمزدلفة من بعد غروب شمس يوم عرفة، وتمتد إلى ما قبل التوجه إلى منى في اليوم العاشر من ذي الحجة.
```

Context state:

```text
muzdalifah_night_state
```

Expected need:

```text
Rest + Ritual Reassurance
```

### Days of Tashreeq

The Days of Tashreeq are modeled as the eleventh, twelfth, and thirteenth days of Dhu al-Hijjah. They are associated with Mina and Jamarat-related activity.

Arabic definition:

```text
أيام التشريق هي الحادي عشر والثاني عشر والثالث عشر من شهر ذي الحجة.
```

Context state:

```text
tashreeq_days_state
```

Expected need:

```text
Ritual Guidance + Crowd Awareness
```

## Places

### MosquePlace

`MosquePlace` represents مسجد / mosque as a general concept. It is used for Quran references that apply to any mosque rather than one specific mosque.

Alternative labels:

```text
Masjid
Mosque
المسجد
المساجد
```

### MakkahCity

`MakkahCity` represents مكة / Makkah. It contains the main Makkah and Hajj place concepts used by the ontology, including Al-Haram, the Kaaba, Mataf, Safa and Marwa, Maqam Ibrahim, the Black Stone, Zamzam Well, the Yemeni Corner, Al-Multazam, Al-Hijr, Arafat, Muzdalifah, Mina, and Jamarat.

Alternative labels:

```text
Mecca
Makkah al-Mukarramah
مكة المكرمة
بكة
أم القرى
البلد الحرام
البلد الأمين
```

Relation:

```text
MakkahCity contains_place AlHaramPlace
AlHaramPlace located_in_city MakkahCity
MakkahCity contains_place MaqamIbrahimPlace
MakkahCity contains_place BlackStonePlace
MakkahCity contains_place ZamzamWellPlace
MakkahCity contains_place YemeniCornerPlace
MakkahCity contains_place MultazamPlace
AlHaramPlace has_gate ZoneSemantic_bab_al_salam_haram
ZoneSemantic_bab_al_salam_haram gate_of AlHaramPlace
```

### MadinahCity

`MadinahCity` represents المدينة المنورة / Madinah. It contains the Prophet's Mosque place concept used for the Madinah visit stage.

Alternative labels:

```text
Medina
Al Madinah
Madinah al-Munawwarah
المدينة
طيبة
مدينة الرسول
يثرب
```

Relation:

```text
MadinahCity contains_place ProphetMosquePlace
ProphetMosquePlace located_in_city MadinahCity
ProphetMosquePlace has_gate ZoneSemantic_bab_quba_prophet_mosque
ZoneSemantic_bab_quba_prophet_mosque gate_of ProphetMosquePlace
```

### ArafatPlace

`ArafatPlace` represents the Hajj place associated with the Arafat-related geofences. Its Arabic label is `عرفات`, and it also has the alternative Arabic label `عرفة`.

Alternative labels:

```text
Arafah
Plain of Arafat
عرفة
```

### MuzdalifahPlace

`MuzdalifahPlace` represents the Hajj place associated with spending the night in Muzdalifah after Arafat. It is linked to the `muzdalifah` and `mashair_train_muzdalifah_station` spatial zones.

Alternative labels:

```text
Al-Mash'ar Al-Haram
Al-Mashar Al-Haram
المشعر الحرام
```

### AlHijrPlace

`AlHijrPlace` represents حِجر إسماعيل, the sacred space adjacent to the Kaaba. It is also known as Al-Hijr and Hateem.

Alternative labels:

```text
Al-Hijr
Hateem
Hijr Ismail
الحِجر
الحطيم
```

### BlackStonePlace

`BlackStonePlace` represents الحجر الأسود / Black Stone, a sacred landmark set in the Kaaba and associated with Tawaf orientation and greeting gestures.

Relation:

```text
BlackStonePlace part_of KaabaPlace
BlackStonePlace located_in_city MakkahCity
MakkahCity contains_place BlackStonePlace
```

### ZamzamWellPlace

`ZamzamWellPlace` represents بئر زمزم / Zamzam Well, the blessed well in Al-Haram near the Kaaba.

Relation:

```text
ZamzamWellPlace part_of AlHaramPlace
ZamzamWellPlace located_in_city MakkahCity
MakkahCity contains_place ZamzamWellPlace
```

### YemeniCornerPlace

`YemeniCornerPlace` represents الركن اليماني / Yemeni Corner, a sacred landmark of the Kaaba encountered during Tawaf. It also includes the Arabic alternative label `الحجر اليماني`.

Relation:

```text
YemeniCornerPlace part_of KaabaPlace
YemeniCornerPlace located_in_city MakkahCity
MakkahCity contains_place YemeniCornerPlace
```

### MultazamPlace

`MultazamPlace` represents الملتزم / Al-Multazam, the area of the Kaaba wall between the Black Stone and the Kaaba door.

Relation:

```text
MultazamPlace part_of KaabaPlace
MultazamPlace located_in_city MakkahCity
MakkahCity contains_place MultazamPlace
```

### MaqamIbrahimPlace

`MaqamIbrahimPlace` represents مقام إبراهيم / Maqam Ibrahim, a sacred place in Al-Haram near the Kaaba.

Alternative labels:

```text
Station of Ibrahim
Maqam Ibrahim
مقام إبراهيم
```

Relation:

```text
MaqamIbrahimPlace part_of AlHaramPlace
MaqamIbrahimPlace located_in_city MakkahCity
MakkahCity contains_place MaqamIbrahimPlace
```

## Quran References

### QuranVerse_2_125

`QuranVerse_2_125` represents البقرة 125 / Al-Baqarah 2:125.

Relations:

```text
MaqamIbrahimPlace mentioned_in_quran QuranVerse_2_125
QuranVerse_2_125 mentions_concept MaqamIbrahimPlace
```

### QuranVerse_2_158

`QuranVerse_2_158` represents البقرة 158 / Al-Baqarah 2:158.

Relations:

```text
SafaMarwa mentioned_in_quran QuranVerse_2_158
ZoneSemantic_safa mentioned_in_quran QuranVerse_2_158
ZoneSemantic_marwah mentioned_in_quran QuranVerse_2_158
QuranVerse_2_158 mentions_concept SafaMarwa
QuranVerse_2_158 mentions_concept ZoneSemantic_safa
QuranVerse_2_158 mentions_concept ZoneSemantic_marwah
```

### QuranVerse_2_198

`QuranVerse_2_198` represents البقرة 198 / Al-Baqarah 2:198.

Relations:

```text
ArafatPlace mentioned_in_quran QuranVerse_2_198
StandingInArafat mentioned_in_quran QuranVerse_2_198
QuranVerse_2_198 mentions_concept ArafatPlace
QuranVerse_2_198 mentions_concept StandingInArafat
```

### QuranVerse_3_96

`QuranVerse_3_96` represents آل عمران 96 / Ali Imran 3:96.

Relations:

```text
MakkahCity mentioned_in_quran QuranVerse_3_96
QuranVerse_3_96 mentions_concept MakkahCity
```

### QuranVerse_3_97

`QuranVerse_3_97` represents آل عمران 97 / Ali Imran 3:97.

Relations:

```text
MaqamIbrahimPlace mentioned_in_quran QuranVerse_3_97
QuranVerse_3_97 mentions_concept MaqamIbrahimPlace
```

### QuranVerse_5_95

`QuranVerse_5_95` represents المائدة 95 / Al-Maidah 5:95.

Relations:

```text
AlIhram mentioned_in_quran QuranVerse_5_95
QuranVerse_5_95 mentions_concept AlIhram
```

### QuranVerse_7_31

`QuranVerse_7_31` represents الأعراف 31 / Al-A'raf 7:31.

Relations:

```text
MosquePlace mentioned_in_quran QuranVerse_7_31
QuranVerse_7_31 mentions_concept MosquePlace
```

### QuranVerse_14_37

`QuranVerse_14_37` represents إبراهيم 37 / Ibrahim 14:37.

Relations:

```text
MakkahCity mentioned_in_quran QuranVerse_14_37
QuranVerse_14_37 mentions_concept MakkahCity
```

### QuranVerse_22_27

`QuranVerse_22_27` represents الحج 27 / Al-Hajj 22:27.

Relations:

```text
HajjJourney mentioned_in_quran QuranVerse_22_27
QuranVerse_22_27 mentions_concept HajjJourney
```

### QuranVerse_24_36

`QuranVerse_24_36` represents النور 36 / An-Nur 24:36.

Relations:

```text
MosquePlace mentioned_in_quran QuranVerse_24_36
QuranVerse_24_36 mentions_concept MosquePlace
```

## Ontology Role in Ouns

The ontology acts as a semantic layer between the Spatial Intelligence Engine and the Contextual Intelligence Engine. The spatial engine detects measurable signals such as boundary entry, movement pattern, direction, and stopping behavior. The ontology defines how these signals relate to pilgrimage concepts such as Ihram, Tawaf, Sa'i, Day of Arafat, Eid al-Adha, and Days of Tashreeq.

This allows the Contextual Intelligence Engine to infer a structured `User Context State`, including the current stage, ritual phase, inferred need, priority, and recommended message type.
