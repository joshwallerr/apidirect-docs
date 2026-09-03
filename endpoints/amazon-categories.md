# Amazon Category IDs

Category slugs for the `category_id` parameter on [Product Search](/docs/amazon-products) and the `category` parameter on [Best Sellers](/docs/amazon-best-sellers). Categories are marketplace-specific — use the table for the `country` you pass in the request.

## Using a category ID

### Example: search laptops in Electronics

```bash
curl "https://apidirect.io/v1/amazon/products?query=laptop&category_id=electronics" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Example: Best Sellers in Software

```bash
curl "https://apidirect.io/v1/amazon/best-sellers?category=software" \
  -H "X-API-Key: YOUR_API_KEY"
```

Product Search also accepts numeric category node IDs (from any Amazon URL's `?node=` parameter) via the `category` parameter — those are not listed here.

### United States (`country=us`)

| Category | ID |
|----------|-----|
| All Departments | `aps` |
| Alexa Skills | `alexa-skills` |
| Amazon Devices | `amazon-devices` |
| Amazon Explore | `live-explorations` |
| Amazon Fresh | `amazonfresh` |
| Amazon Pharmacy | `amazon-pharmacy` |
| Amazon Warehouse | `warehouse-deals` |
| Appliances | `appliances` |
| Apps & Games | `mobile-apps` |
| Arts, Crafts & Sewing | `arts-crafts` |
| Audible Books & Originals | `audible` |
| Automotive Parts & Accessories | `automotive` |
| AWS Courses | `courses` |
| Baby | `baby-products` |
| Beauty & Personal Care | `beauty` |
| Books | `stripbooks` |
| CDs & Vinyl | `popular` |
| Cell Phones & Accessories | `mobile` |
| Clothing, Shoes & Jewelry | `fashion` |
|    Women | `fashion-womens` |
|    Men | `fashion-mens` |
|    Girls | `fashion-girls` |
|    Boys | `fashion-boys` |
|    Baby | `fashion-baby` |
| Collectibles & Fine Art | `collectibles` |
| Computers | `computers` |
| Credit and Payment Cards | `financial` |
| Digital Educational Resources | `edu-alt-content` |
| Digital Music | `digital-music` |
| Electronics | `electronics` |
| Garden & Outdoor | `lawngarden` |
| Gift Cards | `gift-cards` |
| Grocery & Gourmet Food | `grocery` |
| Handmade | `handmade` |
| Health, Household & Baby Care | `hpc` |
| Home & Business Services | `local-services` |
| Home & Kitchen | `garden` |
| Industrial & Scientific | `industrial` |
| Just for Prime | `prime-exclusive` |
| Kindle Store | `digital-text` |
| Luggage & Travel Gear | `fashion-luggage` |
| Luxury Stores | `luxury` |
| Magazine Subscriptions | `magazines` |
| Movies & TV | `movies-tv` |
| Musical Instruments | `mi` |
| Office Products | `office-products` |
| Pet Supplies | `pets` |
| Premium Beauty | `luxury-beauty` |
| Prime Video | `instant-video` |
| Smart Home | `smart-home` |
| Software | `software` |
| Sports & Outdoors | `sporting` |
| Subscribe & Save | `specialty-aps-sns` |
| Subscription Boxes | `subscribe-with-amazon` |
| Tools & Home Improvement | `tools` |
| Toys & Games | `toys-and-games` |
| Under $10 | `under-ten-dollars` |
| Video Games | `videogames` |
| Whole Foods Market | `wholefoods` |

### Australia (`country=au`)

| Category | ID |
|----------|-----|
| All Departments | `aps` |
| Alexa Skills | `alexa-skills` |
| Amazon Devices | `amazon-devices` |
| Amazon Global Store | `amazon-global-store` |
| Apps & Games | `mobile-apps` |
| Audible Audiobooks | `audible` |
| Automotive | `automotive` |
| Baby | `baby` |
| Beauty | `beauty` |
| Books | `stripbooks` |
| CDs & Vinyl | `popular` |
| Clothing, Shoes & Accessories | `fashion` |
|    Women | `fashion-womens` |
|    Men | `fashion-mens` |
|    Girls | `fashion-girls` |
|    Boys | `fashion-boys` |
|    Baby | `fashion-baby` |
| Amazon Warehouse | `warehouse-deals` |
| Computers | `computers` |
| Electronics | `electronics` |
| Garden | `garden` |
| Gift Cards | `gift-cards` |
| Health, Household & Personal Care | `hpc` |
| Home | `home` |
| Home Improvement | `home-improvement` |
| Kindle Store | `digital-text` |
| Kitchen & Dining | `kitchen` |
| Luggage & Travel Gear | `fashion-luggage` |
| Movies & TV | `movies-tv` |
| Musical Instruments | `mi` |
| Pantry Food & Drinks | `grocery` |
| Pet Supplies | `pets` |
| Premium Beauty | `luxury-beauty` |
| Prime Video | `instant-video` |
| Software | `software` |
| Sports, Fitness & Outdoors | `sporting` |
| Stationery & Office Products | `office-products` |
| Toys & Games | `toys` |
| Video Games | `videogames` |
| Wine, Beer & Spirits | `alcohol` |

### Belgium (`country=be`)

| Category | ID |
|----------|-----|
| Toutes nos catégories | `aps` |
| Alimentation | `grocery` |
| Animalerie | `pets` |
| Appareils Amazon | `amazon-devices` |
| Arts, artisanat et couture | `arts-crafts` |
| Auto et Moto | `automotive` |
| Bagages | `luggage` |
| Beauté | `beauty` |
| Boutique chèques-cadeaux | `gift-cards` |
| Bricolage | `home-improvement` |
| Bébé | `baby` |
| DVD & Blu-ray | `movies-tv` |
| High-Tech | `electronics` |
| Hygiène & Santé | `hpc` |
| Industrie & Science | `industrial` |
| Instruments de musique | `mi` |
| Jardin | `garden` |
| Jeux & Jouets | `toys` |
| Jeux vidéo | `videogames` |
| Livres | `stripbooks` |
| Logiciels | `software` |
| Maison & Cuisine | `kitchen` |
| Musique | `popular` |
| Ordinateurs | `computers` |
| Produits de bureau | `office-products` |
| Sports & Loisirs | `sporting` |
| Vêtements & Accessoires | `fashion` |

### Brazil (`country=br`)

| Category | ID |
|----------|-----|
| Todos os departamentos | `aps` |
| Alexa Skills | `alexa-skills` |
| Alimentos e Bebidas | `grocery` |
| Apps e Jogos | `mobile-apps` |
| Automotivo | `automotive` |
| Bebês | `baby` |
| Beleza | `beauty` |
| Bolsas, Malas e Mochilas | `fashion-luggage` |
| Brinquedos e Jogos | `toys` |
| Casa | `home` |
| CD e Vinil | `popular` |
| Computadores e Informática | `computers` |
| Cozinha | `kitchen` |
| Dispositivos Amazon | `amazon-devices` |
| DVD e Blu-Ray | `dvd` |
| Eletrodomésticos | `appliances` |
| Eletrônicos | `electronics` |
| Esportes e Aventura | `sporting` |
| Ferramentas e Materiais de Construção | `hi` |
| Games | `videogames` |
| Instrumentos Musicais | `mi` |
| Jardim e Piscina | `garden` |
| Livros | `stripbooks` |
| Loja Kindle | `digital-text` |
| Material para Escritório e Papelaria | `office-products` |
| Móveis e Decoração | `furniture` |
| Pet Shop | `pets` |
| Prime Video | `instant-video` |
| Roupas, Calçados e Joias | `fashion` |
|    Feminino | `fashion-womens` |
|    Masculino | `fashion-mens` |
|    Meninas | `fashion-girls` |
|    Meninos | `fashion-boys` |
|    Bebês | `fashion-baby` |
| Saúde e Cuidados Pessoais | `hpc` |

### Canada (`country=ca`)

| Category | ID |
|----------|-----|
| All Departments | `aps` |
| Audible Audiobooks | `audible` |
| Alexa Skills | `alexa-skills` |
| Amazon Devices | `amazon-devices` |
| Amazon Warehouse Deals | `warehouse-deals` |
| Apps & Games | `mobile-apps` |
| Automotive | `automotive` |
| Baby | `baby` |
| Beauty | `beauty` |
| Books | `stripbooks` |
| Music | `popular` |
| Clothing, Shoes & Jewelry | `fashion` |
|    Women | `fashion-womens` |
|    Men | `fashion-mens` |
|    Girls | `fashion-girls` |
|    Boys | `fashion-boys` |
|    Baby | `fashion-baby` |
| Electronics | `electronics` |
| Gift Cards | `gift-cards` |
| Grocery | `grocery` |
| Handmade | `handmade` |
| Health & Personal Care | `hpc` |
| Home & Kitchen | `kitchen` |
| Industrial & Scientific | `industrial` |
| Kindle Store | `digital-text` |
| Luggage & Travel Gear | `fashion-luggage` |
| Luxury Beauty | `luxury-beauty` |
| Movies & TV | `dvd` |
| Musical Instruments, Stage & Studio | `mi` |
| Office Products | `office-products` |
| Patio, Lawn & Garden | `lawngarden` |
| Pet Supplies | `pets` |
| Prime Video | `instant-video` |
| Smart Home | `smart-home` |
| Software | `software` |
| Sports & Outdoors | `sporting` |
| Tools & Home Improvement | `tools` |
| Toys & Games | `toys` |
| Video Games | `videogames` |

### China (`country=cn`)

| Category | ID |
|----------|-----|
| 全部分类 | `aps` |
| Kindle商店 | `digital-text` |
| 亚马逊海外购 | `amazon-global-store` |
| Kindle电子书 | `stripbooks` |
| 游戏/娱乐 | `videogames` |
| 手机/通讯 | `communications` |
| 摄影/摄像 | `photo-video` |
| 电子 | `electronics` |
| 数码影音 | `music-players` |
| 电脑/IT | `computers` |
| 办公用品 | `office-products` |
| 小家电 | `home-appliances` |
|  大家电  | `appliances` |
|  电视/音响  | `audio-visual` |
| 家用 | `home` |
| 家居 | `home-substore` |
| 厨具 | `kitchen` |
| 家居装修 | `home-improvement` |
| 宠物用品 | `pets` |
| 食品 | `grocery` |
| 酒 | `wine` |
| 美容化妆 | `beauty` |
| 个护健康 | `hpc` |
| 母婴用品 | `baby` |
| 玩具 | `toys-and-games` |
| 运动户外休闲 | `sporting` |
| 服饰箱包 | `apparel` |
| 鞋靴 | `shoes` |
| 钟表 | `watches` |
| 珠宝首饰 | `jewelry` |
| 汽车用品 | `automotive` |
| 乐器 | `mi` |

### Egypt (`country=eg`)

| Category | ID |
|----------|-----|
| جميع الأقسام | `aps` |
| آلات موسيقية | `mi` |
| أجهزة Amazon | `amazon-devices` |
| أدوات وتحسينات المنزل | `home-improvement` |
| أزياء Amazon | `fashion` |
| ألعاب الفيديو | `videogames` |
| الألعاب والدمى | `toys` |
| الإلكترونيات | `electronics` |
| البقالة والطعام الفاخر | `grocery` |
| الجمال والعناية الشخصية | `beauty` |
| الرياضة واللياقة البدنية | `sports` |
| الصناعة والعلم | `industrial` |
| الفنون والحرف والخياطة | `arts-crafts` |
| المنزل والحديقة | `garden` |
| برمجية | `software` |
| طفل | `baby` |
| عروض مستودع أمازون | `warehouse-deals` |
| قطع وإكسسوارات السيارات | `automotive` |
| كتب | `stripbooks` |
| مستلزمات الحيوانات الأليفة | `pets` |
| مستلزمات الرعاية الصحية والأسرة والطفل | `hpc` |
| منتجات المكتب | `office-products` |
| منتجات المنزل | `home` |

### France (`country=fr`)

| Category | ID |
|----------|-----|
| Toutes nos catégories | `aps` |
| Alexa Skills | `alexa-skills` |
| Amazon Global Store | `amazon-global-store` |
| Amazon Warehouse | `warehouse-deals` |
| Animalerie | `pets` |
| Appareils Amazon | `amazon-devices` |
| Applis & Jeux | `mobile-apps` |
| Auto et Moto | `automotive` |
| Bagages | `luggage` |
| Beauté et Parfum | `beauty` |
| Beauté Premium | `luxury-beauty` |
| Bijoux | `jewelry` |
| Boutique chèques-cadeaux | `gift-cards` |
| Boutique Kindle | `digital-text` |
| Bricolage | `diy` |
| Bébés & Puériculture | `baby` |
| Chaussures et Sacs | `shoes` |
| Cuisine & Maison | `kitchen` |
| DVD & Blu-ray | `dvd` |
| Epicerie | `grocery` |
| Fournitures de bureau | `office-products` |
| Gros électroménager | `appliances` |
| Handmade | `handmade` |
| High-Tech | `electronics` |
| Hygiène et Santé | `hpc` |
| Informatique | `computers` |
| Instruments de musique & Sono | `mi` |
| Jardin | `garden` |
| Jeux et Jouets | `toys` |
| Jeux vidéo | `videogames` |
| Livres | `stripbooks` |
| Livres audio Audible | `audible` |
| Logiciels | `software` |
| Luminaires et Eclairage | `lighting` |
| Mode | `fashion` |
| Moins de 10€ | `under-ten-dollars` |
| Montres | `watches` |
| Musique : CD & Vinyles | `popular` |
| Musique classique | `classical` |
| Prime Video | `instant-video` |
| Secteur industriel et scientifique | `industrial` |
| Sports et Loisirs | `sports` |
| Téléchargement de musique | `digital-music` |
| Ventes Flash Black Friday | `black-friday` |
| Vêtements et accessoires | `clothing` |

### Germany (`country=de`)

| Category | ID |
|----------|-----|
| Alle Kategorien | `aps` |
| Alexa Skills | `alexa-skills` |
| Amazon Geräte | `amazon-devices` |
| Amazon Global Store | `amazon-global-store` |
| Amazon Warehouse | `warehouse-deals` |
| Apps & Spiele | `mobile-apps` |
| Audible Hörbücher | `audible` |
| Auto & Motorrad | `automotive` |
| Baby | `baby` |
| Baumarkt | `diy` |
| Beauty | `beauty` |
| Bekleidung | `clothing` |
| Beleuchtung | `lighting` |
| Black Friday | `black-friday` |
| Bücher | `stripbooks` |
| Bürobedarf & Schreibwaren | `office-products` |
| Computer & Zubehör | `computers` |
| Drogerie & Körperpflege | `drugstore` |
| DVD & Blu-ray | `dvd` |
| Elektro-Großgeräte | `appliances` |
| Elektronik & Foto | `electronics` |
| Fashion | `fashion` |
| Games | `videogames` |
| Garten | `outdoor` |
| Geschenkgutscheine | `gift-cards` |
| Gewerbe, Industrie & Wissenschaft | `industrial` |
| Handmade | `handmade` |
| Haustier | `pets` |
| Home & Business Services | `local-services` |
| Kamera & Foto | `photo` |
| Kindle-Shop | `digital-text` |
| Klassik | `classical` |
| Koffer, Rucksäcke & Taschen  | `luggage` |
| Küche, Haushalt & Wohnen | `kitchen` |
| Lebensmittel & Getränke | `grocery` |
| Musik-CDs & Vinyl | `popular` |
| Musik-Downloads | `digital-music` |
| Musikinstrumente & DJ-Equipment | `mi` |
| Premium Beauty | `luxury-beauty` |
| Prime Video | `instant-video` |
| Schmuck | `jewelry` |
| Schuhe & Handtaschen | `shoes` |
| Software | `software` |
| Spielzeug | `toys` |
| Sport & Freizeit | `sports` |
| Uhren | `watches` |
| Zeitschriften | `magazines` |

### India (`country=in`)

| Category | ID |
|----------|-----|
| All Categories | `aps` |
| Deals | `todays-deals` |
| Alexa Skills | `alexa-skills` |
| Amazon Devices | `amazon-devices` |
| Amazon Fashion | `fashion` |
| Amazon Fresh | `nowstore` |
| Amazon Pantry | `pantry` |
| Appliances | `appliances` |
| Apps & Games | `mobile-apps` |
| Baby | `baby` |
| Beauty | `beauty` |
| Books | `stripbooks` |
| Car & Motorbike | `automotive` |
| Clothing & Accessories | `apparel` |
| Collectibles | `collectibles` |
| Computers & Accessories | `computers` |
| Electronics | `electronics` |
| Furniture | `furniture` |
| Garden & Outdoors | `lawngarden` |
| Gift Cards | `gift-cards` |
| Grocery & Gourmet Foods | `grocery` |
| Health & Personal Care | `hpc` |
| Home & Kitchen | `kitchen` |
| Industrial & Scientific | `industrial` |
| Jewellery | `jewelry` |
| Kindle Store | `digital-text` |
| Luggage & Bags | `luggage` |
| Luxury Beauty | `luxury-beauty` |
| Movies & TV Shows | `dvd` |
| Music | `popular` |
| Musical Instruments | `mi` |
| Office Products | `office-products` |
| Pet Supplies | `pets` |
| Prime Video | `instant-video` |
| Shoes & Handbags | `shoes` |
| Software | `software` |
| Sports, Fitness & Outdoors | `sporting` |
| Tools & Home Improvement | `home-improvement` |
| Toys & Games | `toys` |
| Under ₹500 | `under-ten-dollars` |
| Video Games | `videogames` |
| Watches | `watches` |

### Ireland (`country=ie`)

| Category | ID |
|----------|-----|
| All Departments | `aps` |
| Amazon Devices | `amazon-devices` |
| Arts & Crafts | `arts-crafts` |
| Baby | `baby` |
| Beauty | `beauty` |
| Books | `stripbooks` |
| Business & Professional | `industrial` |
| Car & Motorbike | `automotive` |
| CDs & Vinyl | `popular` |
| Computing & Office | `office-products` |
| DIY & Tools | `home-improvement` |
| DVD & Blu-ray | `movies-tv` |
| Electronics | `electronics` |
| Fashion | `fashion` |
| Food & Grocery | `grocery` |
| Garden | `garden` |
| Gift Cards | `gift-cards` |
| Health & Personal Care | `hpc` |
| Home & Kitchen | `home` |
| Musical Instruments | `mi` |
| PC & Video Games | `videogames` |
| Pet Supplies | `pets` |
| Software | `software` |
| Sports & Outdoors | `sporting` |
| Toys & Games | `toys` |

### Italy (`country=it`)

| Category | ID |
|----------|-----|
| Tutte le categorie | `aps` |
| Abbigliamento | `apparel` |
| Alexa Skill | `alexa-skills` |
| Alimentari e cura della casa | `grocery` |
| Amazon Global Store | `amazon-global-store` |
| Amazon Warehouse | `warehouse-deals` |
| App e Giochi | `mobile-apps` |
| Audiolibri Audible | `audible` |
| Auto e Moto - Parti e Accessori | `automotive` |
| Bellezza | `beauty` |
| Buoni Regalo | `gift-cards` |
| Cancelleria e prodotti per ufficio | `office-products` |
| Casa e cucina | `kitchen` |
| CD e Vinili  | `popular` |
| Dispositivi Amazon | `amazon-devices` |
| Elettronica | `electronics` |
| Fai da te | `diy` |
| Film e TV | `dvd` |
| Giardino e giardinaggio | `garden` |
| Giochi e giocattoli | `toys` |
| Gioielli | `jewelry` |
| Grandi elettrodomestici | `appliances` |
| Handmade | `handmade` |
| Illuminazione | `lighting` |
| Industria e Scienza | `industrial` |
| Informatica | `computers` |
| Kindle Store | `digital-text` |
| Libri | `stripbooks` |
| Meno di 10€ | `under-ten-dollars` |
| Moda | `fashion` |
| Black Friday | `black-friday` |
| Musica Digitale | `digital-music` |
| Orologi | `watches` |
| Prima infanzia | `baby` |
| Prime Video | `instant-video` |
| Prodotti per animali domestici | `pets` |
| Salute e cura della persona | `hpc` |
| Scarpe e borse | `shoes` |
| Software | `software` |
| Sport e tempo libero | `sporting` |
| Strumenti musicali e DJ | `mi` |
| Valigeria | `luggage` |
| Videogiochi | `videogames` |

### Japan (`country=jp`)

| Category | ID |
|----------|-----|
| すべてのカテゴリー | `aps` |
| Audible・オーディオブック | `audible` |
| Amazon デバイス | `amazon-devices` |
| Kindleストア  | `digital-text` |
| Prime Video | `instant-video` |
| Alexaスキル | `alexa-skills` |
| デジタルミュージック | `digital-music` |
| Android アプリ | `mobile-apps` |
| 本 | `stripbooks` |
| 洋書 | `english-books` |
| ミュージック | `popular` |
| クラシック | `classical` |
| DVD | `dvd` |
| TVゲーム | `videogames` |
| PCソフト | `software` |
| パソコン・周辺機器 | `computers` |
| 家電&カメラ | `electronics` |
| 文房具・オフィス用品 | `office-products` |
| ホーム&キッチン | `kitchen` |
| ペット用品 | `pets` |
| ドラッグストア | `hpc` |
| ビューティー | `beauty` |
| 食品・飲料・お酒 | `food-beverage` |
| ベビー&マタニティ | `baby` |
| ファッション | `fashion` |
|    レディース | `fashion-womens` |
|    メンズ | `fashion-mens` |
|    キッズ＆ベビー | `fashion-baby-kids` |
| 服＆ファッション小物 | `apparel` |
| シューズ＆バッグ | `shoes` |
| 腕時計 | `watch` |
| ジュエリー | `jewelry` |
| おもちゃ | `toys` |
| ホビー | `hobby` |
| 楽器 | `mi` |
| スポーツ&アウトドア | `sporting` |
| 車＆バイク | `automotive` |
| DIY・工具・ガーデン | `diy` |
| 大型家電 | `appliances` |
| クレジットカード | `financial` |
| ギフト券 | `gift-cards` |
| 産業・研究開発用品 | `industrial` |
| Amazonアウトレット | `warehouse-deals` |

### Mexico (`country=mx`)

| Category | ID |
|----------|-----|
| Todos los departamentos | `aps` |
| Alexa Skills | `alexa-skills` |
| Auto | `automotive` |
| Bebé | `baby` |
| Belleza | `beauty` |
| Belleza Premium | `luxury-beauty` |
| Dispositivos de Amazon | `amazon-devices` |
| Electrónicos | `electronics` |
| Películas y Series de TV | `dvd` |
| Prime Video | `instant-video` |
| Tienda Kindle | `digital-text` |
| Ropa, Zapatos y Accesorios | `fashion` |
|    Mujeres | `fashion-womens` |
|    Hombres | `fashion-mens` |
|    Niñas | `fashion-girls` |
|    Niños | `fashion-boys` |
|    Bebé | `fashion-baby` |
| Alimentos y Bebidas | `grocery` |
| Deportes y Aire Libre | `sporting` |
| Hecho a mano | `handmade` |
| Herramientas y Mejoras del Hogar | `hi` |
| Hogar y Cocina | `kitchen` |
| Industria y ciencia | `industrial` |
| Instrumentos musicales | `mi` |
| Jardín | `garden` |
| Juegos y juguetes | `toys` |
| Libros | `stripbooks` |
| Mascotas | `pets` |
| Música | `popular` |
| Oficina y Papelería | `office-products` |
| Remates de Almacén | `warehouse-deals` |
| Salud y Cuidado Personal | `hpc` |
| Software | `software` |
| Tarjetas de Regalo | `gift-cards` |
| Videojuegos | `videogames` |

### Netherlands (`country=nl`)

| Category | ID |
|----------|-----|
| Alle afdelingen | `aps` |
| Amazon Warehouse | `warehouse-deals` |
| Amazon-apparaten | `amazon-devices` |
| Auto en motor | `automotive` |
| Babyproducten | `baby` |
| Beauty en persoonlijke verzorging | `beauty` |
| Black Friday | `black-friday` |
| Boeken | `stripbooks` |
| Cadeaubonnen | `gift-cards` |
| Cd's en lp's | `popular` |
| Elektronica | `electronics` |
| Films en tv | `dvd` |
| Gezondheid en persoonlijke verzorging | `hpc` |
| Huisdierbenodigdheden | `pets` |
| Kantoorproducten | `office-products` |
| Kindle Store | `digital-text` |
| Kleding, schoenen en sieraden | `fashion` |
| Klussen en gereedschap | `home-improvement` |
| Levensmiddelen | `grocery` |
| Muziekinstrumenten | `mi` |
| Overig | `misc` |
| Prime Video | `instant-video` |
| Software | `software` |
| Speelgoed en spellen | `toys` |
| Sport en outdoor | `sports` |
| Tuin, terras en gazon | `outdoor` |
| Videogames | `videogames` |
| Wonen en keuken | `home` |
| Zakelijk, industrie en wetenschap | `industrial` |

### Poland (`country=pl`)

| Category | ID |
|----------|-----|
| Wszystkie kategorie | `aps` |
| Arts & crafts | `arts-crafts` |
| Biuro | `office-products` |
| Biznes, przemysł i nauka | `industrial` |
| Dom i kuchnia | `home` |
| Dziecko | `baby` |
| Elektronika | `electronics` |
| Filmy i programy TV | `movies-tv` |
| Gry wideo | `videogames` |
| Instrumenty muzyczne | `mi` |
| Karty podarunkowe | `gift-cards` |
| Komputery i akcesoria | `computers` |
| Książki | `stripbooks` |
| Motoryzacja | `automotive` |
| Muzyka | `popular` |
| Odzież, obuwie i akcesoria | `fashion` |
| Ogród | `garden` |
| Oprogramowanie | `software` |
| Renowacja domu | `home-improvement` |
| Sport i turystyka | `sporting` |
| Uroda | `beauty` |
| Urządzenia Amazon | `amazon-devices` |
| Zabawki i gry | `toys` |
| Zdrowie i gospodarstwo domowe | `hpc` |
| Zwierzęta | `pets` |

### Saudi Arabia (`country=sa`)

| Category | ID |
|----------|-----|
| جميع الأقسام | `aps` |
| آلات موسيقية | `mi` |
| أجهزة Amazon | `amazon-devices` |
| أدوات وتحسينات المنزل | `home-improvement` |
| أزياء Amazon | `fashion` |
| ألعاب الفيديو | `videogames` |
| الأجهزة المنزلية | `appliances` |
| الألعاب والدمى | `toys` |
| الإلكترونيات | `electronics` |
| البقالة والطعام الفاخر | `grocery` |
| الجمال والعناية الشخصية | `beauty` |
| الرياضة واللياقة البدنية | `sports` |
| الصناعة والعلم | `industrial` |
| الفنون والحرف والخياطة | `arts-crafts` |
| المطبخ والطعام | `kitchen` |
| المنزل والحديقة | `garden` |
| برايم فيديو | `instant-video` |
| بطاقات الهدايا | `gift-cards` |
| طفل | `baby` |
| عروض مستودع أمازون | `warehouse-deals` |
| قطع وإكسسوارات السيارات | `automotive` |
| كتب | `stripbooks` |
| متجر أمازون العالمي | `amazon-global-store` |
| مستلزمات الحيوانات الأليفة | `pets` |
| مستلزمات الرعاية الصحية والأسرة والطفل | `hpc` |
| منتجات المكتب | `office-products` |
| منتجات المنزل | `home` |

### Singapore (`country=sg`)

| Category | ID |
|----------|-----|
| Gift Cards | `gift-cards` |
| All Departments | `aps` |
| Amazon International Store | `amazon-global-store` |
| Automotive | `automotive` |
| Baby | `baby` |
| Beauty & Personal Care | `beauty` |
| Books | `stripbooks` |
| CDs & Vinyl | `popular` |
| Clothing, Shoes & Jewellery | `fashion` |
| Computer & Accessories | `computers` |
| Electronics | `electronics` |
| Garden & Outdoor | `lawngarden` |
| Grocery | `grocery` |
| Health, Household & Personal Care | `hpc` |
| Home | `home` |
| Industrial & Scientific | `industrial` |
| Kitchen & Dining | `kitchen` |
| Luggage & Travel Gear | `fashion-luggage` |
| Luxury Beauty | `luxury-beauty` |
| Movies & TV | `movies-tv` |
| Musical Instruments | `mi` |
| Office Products | `office-products` |
| Pet Supplies | `pets` |
| Prime Video | `instant-video` |
| Software | `software` |
| Sports & Outdoors | `sporting` |
| Tools & Home Improvement | `home-improvement` |
| Toys & Games | `toys` |
| Video Games | `videogames` |

### South Africa (`country=za`)

| Category | ID |
|----------|-----|
| All Departments | `aps` |
| Arts, Crafts & Sewing | `arts-crafts` |
| Baby | `baby` |
| Beauty | `beauty` |
| Books | `stripbooks` |
| Electronics & Photo | `electronics` |
| Gift Cards | `gift-cards` |
| Health & Personal Care | `hpc` |
| Home & Kitchen | `home` |
| Home Improvement | `home-improvement` |
| Office Products | `office-products` |
| Pet Supplies | `pets` |
| Sports & Outdoors | `sporting` |
| Toys & Games | `toys` |
| Video Games | `videogames` |

### Spain (`country=es`)

| Category | ID |
|----------|-----|
| Todos los departamentos | `aps` |
| Alexa Skills | `alexa-skills` |
| Alimentación y bebidas | `grocery` |
| Amazon Global Store | `amazon-global-store` |
| Amazon Warehouse | `warehouse-deals` |
| Appstore para Android | `mobile-apps` |
| Audible audiolibros y podcasts exclusivos | `audible` |
| Bebé | `baby` |
| Belleza | `beauty` |
| Black Friday | `black-friday` |
| Bricolaje y herramientas | `diy` |
| Cheques regalo | `gift-cards` |
| Coche y Moto - Piezas y accesorios | `automotive` |
| Deportes y aire libre | `sporting` |
| Dispositivos de Amazon | `amazon-devices` |
| Electrónica | `electronics` |
| Equipaje | `luggage` |
| Grandes electrodomésticos | `appliances` |
| Handmade | `handmade` |
| Hogar y cocina | `kitchen` |
| Iluminación | `lighting` |
| Industria y ciencia | `industrial` |
| Informática | `computers` |
| Instrumentos musicales | `mi` |
| Jardín | `lawngarden` |
| Joyería | `jewelry` |
| Juguetes y juegos | `toys` |
| Libros | `stripbooks` |
| Menos de 10€ | `under-ten-dollars` |
| Moda | `fashion` |
| Música Digital | `digital-music` |
| Música: CDs y vinilos | `popular` |
| Oficina y papelería | `office-products` |
| Películas y TV | `dvd` |
| Prime Video | `instant-video` |
| Productos para mascotas | `pets` |
| Relojes | `watches` |
| Ropa y accesorios | `apparel` |
| Salud y cuidado personal | `hpc` |
| Software | `software` |
| Tienda Kindle | `digital-text` |
| Videojuegos | `videogames` |
| Zapatos y complementos | `shoes` |

### Sweden (`country=se`)

| Category | ID |
|----------|-----|
| Alla kategorier | `aps` |
| Amazon-enheter | `amazon-devices` |
| Babyprodukter | `baby` |
| Bygg, el & verktyg | `home-improvement` |
| Böcker | `stripbooks` |
| Elektronik | `electronics` |
| Film & TV-serier | `movies-tv` |
| Fordon | `automotive` |
| Hem & kök | `home` |
| Hobby & hantverk | `arts-crafts` |
| Husdjursprodukter | `pets` |
| Hälsa, vård & hushåll | `hpc` |
| Industriella verktyg & produkter | `industrial` |
| Kläder, skor & accessoarer | `fashion` |
| Kontorsprodukter & skolmaterial | `office-products` |
| Leksaker & spel | `toys` |
| Livsmedel och gourmetmat | `grocery` |
| Musik | `popular` |
| Musikinstrument | `mi` |
| Presentkort | `gift-cards` |
| Prime Video | `instant-video` |
| Programvara | `software` |
| Skönhet & kroppsvård | `beauty` |
| Sport & outdoor | `sporting` |
| Trädgård | `garden` |
| TV-spel & konsoler | `videogames` |

### Turkey (`country=tr`)

| Category | ID |
|----------|-----|
| Tüm Kategoriler | `aps` |
| Bahçe | `garden` |
| Bebek | `baby` |
| Bilgisayarlar | `computers` |
| Elektronik | `electronics` |
| Ev | `home` |
| Ev ve Mutfak | `kitchen` |
| Evcil Hayvan Malzemeleri | `pets` |
| Gıda ve İçecek | `grocery` |
| Hediye Kartları | `gift-cards` |
| Kitaplar | `stripbooks` |
| Kişisel Bakım ve Kozmetik | `beauty` |
| Moda | `fashion` |
| Müzik Aletleri | `mi` |
| Ofis Ürünleri | `office-products` |
| Oyuncaklar ve Oyunlar | `toys` |
| PC ve Video Oyunları | `videogames` |
| Prime Video | `instant-video` |
| Sağlık ve Bakım | `hpc` |
| Spor | `sports` |
| Yapı Market | `diy` |

### United Arab Emirates (`country=ae`)

| Category | ID |
|----------|-----|
| All Categories | `aps` |
| Amazon Devices | `amazon-devices` |
| Amazon Fashion | `fashion` |
| Amazon Global Store | `amazon-global-store` |
| Amazon Warehouse | `warehouse-deals` |
| Appliances | `appliances` |
| Automotive Parts & Accessories | `automotive` |
| Baby | `baby` |
| Beauty & Personal Care | `beauty` |
| Books | `stripbooks` |
| Computer & Accessories | `computers` |
| Electronics | `electronics` |
| Gift Cards | `gift-cards` |
| Grocery & Gourmet Food | `grocery` |
| Health, Household & Baby Care | `hpc` |
| Home & Business Services | `local-services` |
| Home & Garden | `garden` |
| Kitchen & Dining | `kitchen` |
| Luggage & Travel Gear | `fashion-luggage` |
| Musical Instruments | `mi` |
| Office Products | `office-products` |
| Pet Supplies | `pets` |
| Prime Video | `instant-video` |
| Sports | `sports` |
| Tools & Home Improvement | `tools` |
| Toys & Games | `toys` |
| Video Games | `videogames` |

### United Kingdom (`country=gb`)

| Category | ID |
|----------|-----|
| All Departments | `aps` |
| Black Friday | `black-friday` |
| Alexa Skills | `alexa-skills` |
| Amazon Devices | `amazon-devices` |
| Amazon Fresh | `amazonfresh` |
| Amazon Global Store | `amazon-global-store` |
| Amazon Study | `edu-alt-content` |
| Amazon Warehouse | `warehouse-deals` |
| Apps & Games | `mobile-apps` |
| Audible Audiobooks | `audible` |
| Baby | `baby` |
| Beauty | `beauty` |
| Books | `stripbooks` |
| Car & Motorbike | `automotive` |
| CDs & Vinyl | `popular` |
| Classical Music | `classical` |
| Computers & Accessories | `computers` |
| Digital Music | `digital-music` |
| DIY & Tools | `diy` |
| DVD & Blu-ray | `dvd` |
| Electronics & Photo | `electronics` |
| Fashion | `fashion` |
|    Women | `fashion-womens` |
|    Men | `fashion-mens` |
|    Girls | `fashion-girls` |
|    Boys | `fashion-boys` |
|    Baby | `fashion-baby` |
| Garden & Outdoors | `outdoor` |
| Gift Cards | `gift-cards` |
| Grocery | `grocery` |
| Handmade | `handmade` |
| Health & Personal Care | `drugstore` |
| Home & Business Services | `local-services` |
| Home & Kitchen | `kitchen` |
| Industrial & Scientific | `industrial` |
| Kindle Store | `digital-text` |
| Large Appliances | `appliances` |
| Lighting | `lighting` |
| Luggage and travel gear | `fashion-luggage` |
| Luxury Stores | `luxury` |
| Morrisons | `morrisons` |
| Musical Instruments & DJ Equipment | `mi` |
| PC & Video Games | `videogames` |
| Pet Supplies | `pets` |
| Premium Beauty | `luxury-beauty` |
| Prime Video | `instant-video` |
| Software | `software` |
| Sports & Outdoors | `sports` |
| Stationery & Office Supplies | `office-products` |
| Subscribe & Save | `specialty-aps-sns` |
| Toys & Games | `toys` |
