Siin juhend, kuidas seda teha läbi **Google Cloud Console**

See juhend näitab, kuidas seadistada Google Cloud Console'is rakendus, et saada meilide saatmiseks vajalikud võtmed, ning kuidas siduda need WordPressi WP Mail SMTP pistikprogrammiga.

### 1. Uue projekti loomine Google Cloud Console'is
*   **[00:01:16]** Mine Google Cloud Console'i (Project section), vali uue projekti loomise valik (**New Project**).
Esmakordselt sinna lehele minnes küsitakse teie käest nõusolekut.
<img width="423" height="501" alt="image" src="https://github.com/user-attachments/assets/5aa52fef-51ab-4a3a-9043-8ac2ecd77d82" /></br>
Alumisele valikule ei pea linnukest panema, kui sa ei soovi saada perioodiliselt mingeid uudiseid jne.

Kui nõusolek antud, vajuta akna all olevale tekstile **Agree and continue**

Akna ülemises osas on nupp teksti **Select Project**
<img width="595" height="70" alt="image" src="https://github.com/user-attachments/assets/4de0abac-4384-49c4-8143-278f4531aedf" /></br>

Avaneb aken, kus on näha sinu projektid ning uue projekti tegemiseks on valik paremas nurgas üleval **New Project**.
<img width="598" height="175" alt="image" src="https://github.com/user-attachments/assets/20168881-ea9d-42ad-8fac-a064f4f3c91b" /></br>


*   Anna projektile nimi (näiteks E-pood wpdemo1372) ja klõpsa nupule **Create**. See on vajalik eraldi töökeskkonna loomiseks, kus hoitakse meilide saatmiseks vajalikke API seadeid.
<img width="444" height="312" alt="image" src="https://github.com/user-attachments/assets/2b877372-b7e3-4975-9f8b-5df745e516ca" /></br>

Peal **Create** vajutamist tekib paremale nurka teavitus uue projekti loomisest. Vali see ning siis avaneb selle projektiga seotud valikud.
<img width="304" height="139" alt="image" src="https://github.com/user-attachments/assets/8846e6cf-e0e6-4a09-ba5e-0e6cced4ebef" /></br>

<img width="540" height="307" alt="image" src="https://github.com/user-attachments/assets/5b051a7e-f8ac-404d-a70c-41cfb454d9a7" /></br>



### 2. Gmail API lubamine
*   **[00:01:42]** Vali vasakpoolsest menüüst **APIs & Services** (API-d ja teenused) ja klõpsa nupule **Enable APIs and Services**.
*   <img width="361" height="153" alt="image" src="https://github.com/user-attachments/assets/7c0de09a-1e84-4e1d-b7df-313fdd8928c5" /></br>


*   **[00:01:52]** Sisesta otsinguribale "Gmail API", klõpsa õigele tulemusele ja vajuta nuppu **Enable** (Luba). See annab sinu projektile ligipääsu Gmaili meilisaatmise funktsioonidele.

*   <img width="483" height="138" alt="image" src="https://github.com/user-attachments/assets/2caa7ee7-dfba-4c0b-a261-97f01c89bc89" /></br>
<img width="421" height="159" alt="image" src="https://github.com/user-attachments/assets/8e91a93a-97ca-4980-951b-46d464c1899b" /></br>

ja siis vajuta otsingu tulemusena esile tulnud **Gmail API** peale
<img width="234" height="234" alt="image" src="https://github.com/user-attachments/assets/efb54271-a9f8-451c-b0f9-8cff02f5b1b1" /></br>

<img width="362" height="150" alt="image" src="https://github.com/user-attachments/assets/156d6ff9-4fb0-41fe-b21d-1f084e8f546f" /></br>

Skoobi (3.samm) osa võib vahele jätta ja vajutada seal all olevale valikule **Save and continud**
<img width="425" height="44" alt="image" src="https://github.com/user-attachments/assets/3f01ea31-c999-4a16-a192-c16baa936042" /></br>


### 3. Mandaatide (Credentials) loomine
*   **[00:02:06]** Pärast API lubamist suunatakse sind seadete lehele, kus pead vajutama nupule **Create Credentials** (Loo mandaadid).
*   <img width="674" height="212" alt="image" src="https://github.com/user-attachments/assets/1185e9ed-4d23-4c91-80c8-8ec2d0ef2d6e" /></br>

*   **[00:02:22]** Vali rippmenüüst, millist API-t kasutad (**Gmail API**) ja andmete tüübiks **User data** (Kasutaja andmed). Seejärel klõpsa **Next**.
<img width="513" height="442" alt="image" src="https://github.com/user-attachments/assets/c67f1433-a3e0-4a16-a806-6f9baafaa42a" /></br>

### 4. Rakenduse info täitmine (OAuth Consent Screen)
*   **[00:02:35]** Määra **App name** (rakenduse nimi, nt "SMTP" või muu taoline).
*   Vali tugimeiliaadress (**User support email**) ja keri allapoole, et lisada oma meiliaadress ka lahtrisse **Developer contact information**.
*   Salvesta ja jätka (**Save and Continue**).
*   <img width="482" height="595" alt="image" src="https://github.com/user-attachments/assets/dc995a9a-88da-4f13-9c1b-6819576dbd8e" /></br>


### 5. OAuthi kliendi ID seadistamine ja suunav URL
*   **[00:03:05]** Rakenduse tüübiks (**Application type**) vali rippmenüüst **Web application** (Veebirakendus). Vajadusel võid ka sellele sammu jaoks arusaadava nime panna.

*   <img width="432" height="234" alt="image" src="https://github.com/user-attachments/assets/1e65c187-4ee8-41a0-b754-2ccad46bc261" /></br>

*   **[00:03:22]** *See on oluline samm:* Keri allapoole jaotiseni **Authorized redirect URIs** ja klõpsa "Add URI".

*   <img width="412" height="113" alt="image" src="https://github.com/user-attachments/assets/f1cc2928-c43a-4a85-b5a2-5d0d94d7455f" /></br>

*   Mine korraks tagasi WordPressi WP Mail SMTP seadete lehele, kopeeri sealt väljalt *Authorized Redirect URI* antud link ja kleebi see Google Cloud Console'i lahtrisse.

*   <img width="822" height="305" alt="image" src="https://github.com/user-attachments/assets/c8eddc7b-c38b-4eb1-90cd-a5ebdc0e5427" /></br>


<img width="546" height="234" alt="image" src="https://github.com/user-attachments/assets/d3c59e03-f7e3-44d6-8802-bc3ef56b44d3" /></br>


*   Seejärel vajuta **Create** ja pärast ID loomist lihtsalt **Done**.

### 6. Rakenduse avaldamine (Publish App)
*   **[00:03:51]** Enne võtmete kasutamist pead rakenduse avalikustama. Mine vasakpoolsest menüüst lehele **OAuth consent screen->Audience**.
*   Klõpsa nupule **Publish App** (Avaldage rakendus).

*   <img width="458" height="132" alt="image" src="https://github.com/user-attachments/assets/dd2cbf2f-58a0-4ae0-ab5b-9a2f9c088607" /></br>

*   Ilmub hüpikaken, kus kinnita valik vajutades **Confirm**. 

### 7. Client ID ja Client Secret'i kopeerimine
*   **[00:04:09]** Mine vasakpoolsest menüüst tagasi **Credentials** (Mandaadid) lehele.

*   <img width="390" height="162" alt="image" src="https://github.com/user-attachments/assets/12110240-7cbc-4cf4-8421-a58ffa47ccef" /></br>

*   Leiad sealt äsja loodud OAuth 2.0 kliendi. Klõpsa selle kõrval oleval pliiatsikoonil (Muuda/Edit).

*   <img width="911" height="119" alt="image" src="https://github.com/user-attachments/assets/e7fad2bb-2996-4475-ac98-e825ffbbab90" /></br>

*   Nüüd kuvatakse lehel **Client ID** ja **Client secret** koodid. Kopeeri mõlemad ([00:04:20], [00:04:28]).

### 8. WordPressi seadistamine
*   **[00:04:33]** Mine tagasi WordPressi (WP Mail SMTP seadetesse) ja kleebi äsja kopeeritud koodid vastavatesse **Client ID** ja **Client Secret** lahtritesse.

*   <img width="727" height="275" alt="image" src="https://github.com/user-attachments/assets/cac816cf-3d57-4f8a-b5ef-a729409d14cc" /></br>

*   Kerige alla ja vajutage **Save Settings** (Salvesta seaded).

### 9. Google'i kontoga ühendamine ja lubade andmine
*   **[00:04:41]** Nüüd näed WordPressis nuppu kirjaga "Allow plugin to send emails using your Google account". Klõpsa sellele.
*   **[00:04:49]** Sind suunatakse Google'i sisselogimislehele. Vali see sama Google'i konto, millega äsja projekti lõid.
*   Kuna tegemist on sinu isikliku kinnitamata rakendusega, võib Google kuvada hoiatuse ("Google hasn’t verified this app"). Sellisel juhul vajuta **Advanced** (Täpsemalt) ja seejärel **Go to... (unsafe)**.
*   Kinnita juurdepääs, klõpsates **Continue**.

### 10. Lõplik testimine
*   **[00:05:07]** Sind suunatakse tagasi WordPressi. Ekraanil peaks olema kinnitus, et kõik on edukalt ühendatud (Everything is linked).
*   **[00:05:16]** Ühenduse testimiseks vali WP Mail SMTP menüüst vahekaart **Tools** (Tööriistad) või "Email Test".
*   Sisesta suvaline e-posti aadress, kuhu soovid testkirja saata, ja klõpsa **Send Test Email**. Kui kiri jõuab kohale, töötab sinu kodulehe e-kirjade süsteem laitmatult!

Allikas: [How to Set Up Google SMTP in WordPress | Complete Guide](https://www.youtube.com/watch?v=iC1jkQom_nM)</br>
(Ava uues aknas: Ctrl + klõps / Cmd + klõps)
