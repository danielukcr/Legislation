
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>UK Legislation Sections (List)</title>
  <style>
    :root{
      --bg:#0b0f19; --panel:#111827; --panel2:#0f172a;
      --text:#e5e7eb; --muted:#9ca3af; --accent:#60a5fa;
      --border:#263043; --chip:#1f2937;
    }
    *{box-sizing:border-box}
    body{
      margin:0; font-family:system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif;
      background:linear-gradient(180deg,var(--bg),#060813);
      color:var(--text);
    }
    header{
      position:sticky; top:0; z-index:5;
      background:rgba(11,15,25,.85);
      backdrop-filter: blur(10px);
      border-bottom:1px solid var(--border);
    }
    .wrap{max-width:1100px; margin:0 auto; padding:18px 16px}
    h1{margin:0 0 8px; font-size:20px; letter-spacing:.2px}
    .sub{margin:0; color:var(--muted); font-size:13px}
    .toolbar{
      display:flex; gap:10px; flex-wrap:wrap; margin-top:12px;
      align-items:center; justify-content:space-between;
    }
    .search{
      flex: 1 1 420px;
      display:flex; align-items:center; gap:10px;
      background:var(--panel);
      border:1px solid var(--border);
      border-radius:12px; padding:10px 12px;
    }
    .search input{
      width:100%; border:0; outline:0; background:transparent;
      color:var(--text); font-size:14px;
    }
    .btns{display:flex; gap:10px; flex-wrap:wrap}
    button{
      border:1px solid var(--border);
      background:var(--panel);
      color:var(--text);
      padding:10px 12px;
      border-radius:12px;
      cursor:pointer;
      font-size:13px;
    }
    button:hover{border-color:#334155}
    .chips{
      display:flex; gap:8px; flex-wrap:wrap; margin-top:12px;
    }
    .chip{
      display:inline-flex; align-items:center; gap:8px;
      padding:7px 10px;
      border-radius:999px;
      background:var(--chip);
      border:1px solid var(--border);
      color:var(--text);
      font-size:12px;
      cursor:pointer;
      user-select:none;
    }
    .chip[aria-pressed="true"]{border-color:var(--accent); box-shadow:0 0 0 2px rgba(96,165,250,.15)}
    main{padding:18px 0 60px}
    .grid{
      display:grid;
      grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
      gap:14px;
    }
    .card{
      background:linear-gradient(180deg,var(--panel),var(--panel2));
      border:1px solid var(--border);
      border-radius:16px;
      overflow:hidden;
      box-shadow: 0 10px 30px rgba(0,0,0,.25);
    }
    .card header{
      position:unset;
      background:transparent;
      border:0;
      padding:14px 14px 10px;
    }
    .act{
      display:flex; align-items:flex-start; justify-content:space-between; gap:10px;
    }
    .act h2{margin:0; font-size:16px; line-height:1.2}
    .count{color:var(--muted); font-size:12px; white-space:nowrap}
    .list{padding:0 10px 12px}
    details{
      border-top:1px solid rgba(38,48,67,.6);
      padding:10px 6px;
    }
    summary{
      cursor:pointer;
      list-style:none;
      display:flex; align-items:center; justify-content:space-between; gap:10px;
      font-size:13px;
    }
    summary::-webkit-details-marker{display:none}
    .sec{color:var(--text); font-weight:600}
    .desc{color:var(--muted); font-weight:500; margin-left:8px}
    .copyRow{
      display:flex; gap:8px; align-items:center; margin-top:8px; flex-wrap:wrap;
    }
    .mini{
      padding:7px 9px; font-size:12px; border-radius:10px;
      background:#0b1222;
    }
    .mono{
      font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
      font-size:12px; color:#cbd5e1;
      padding:8px 10px; background:#0b1222;
      border:1px solid rgba(38,48,67,.6);
      border-radius:12px;
      overflow:auto;
      max-width:100%;
    }
    .empty{
      margin:18px 0 0;
      padding:14px;
      background:rgba(17,24,39,.6);
      border:1px dashed rgba(38,48,67,.9);
      border-radius:14px;
      color:var(--muted);
      font-size:14px;
    }
    footer{
      color:var(--muted);
      font-size:12px;
      padding-top:16px;
    }
    a{color:var(--accent)}
  </style>
</head>

<body>
<header>
  <div class="wrap">
    <h1>Legislation & Sections</h1>
    <p class="sub">Search, filter by Act, and copy any section reference.</p>

    <div class="toolbar">
      <div class="search" role="search">
        <span aria-hidden="true">🔎</span>
        <input id="q" type="search" placeholder="Search (e.g., 'Section 47', 'knife', 'fraud', 'Firearms Act 1968')…" />
      </div>
      <div class="btns">
        <button id="expandAll" type="button" title="Open all section details">Expand all</button>
        <button id="collapseAll" type="button" title="Close all section details">Collapse all</button>
        <button id="clear" type="button" title="Clear search & filters">Clear</button>
      </div>
    </div>

    <div class="chips" id="chips" aria-label="Act filters"></div>
  </div>
</header>

<main class="wrap">
  <div id="resultsMeta" class="sub" style="margin-bottom:12px;"></div>
  <section class="grid" id="grid" aria-live="polite"></section>
  <div id="empty" class="empty" style="display:none;">No matches. Try a different search term or clear filters.</div>

  <footer class="wrap" style="padding-left:0;padding-right:0;">
    Tip: click an Act chip to filter. Use search to match Act name, section number, or description.
  </footer>
</main>

<script>
  // ---------- DATA ----------
  const acts = [
    {
      act: "Offences against the Person Act 1861",
      sections: [
        { section: "Section 4",  title: "Conspiring or soliciting to commit murder." },
        { section: "Section 5",  title: "Manslaughter." },
        { section: "Section 9",  title: "Murder or manslaughter abroad." },
        { section: "Section 16", title: "Threats to kill." },
        { section: "Section 18", title: "Shooting or attempting to shoot, or wounding with intent to do grievous bodily harm." },
        { section: "Section 20", title: "Inflicting bodily injury, with or without weapon." },
        { section: "Section 21", title: "Attempting to choke, &c. in order to commit any indictable offence." },
        { section: "Section 23", title: "Maliciously administering poison, &c. so as to endanger life or inflict grievous bodily harm." },
        { section: "Section 24", title: "Maliciously administering poison, &c. with intent to injure, aggrieve, or annoy any other person." },
        { section: "Section 27", title: "Exposing children whereby life is endangered." },
        { section: "Section 28", title: "Causing bodily injury by gunpowder." },
        { section: "Section 29", title: "Causing gunpowder to explode, or sending to any person an explosive substance, or throwing corrosive fluid on a person, with intent to do grievous bodily harm." },
        { section: "Section 30", title: "Placing gunpowder near a building, with intent to do bodily injury to any person." },
        { section: "Section 31", title: "Setting spring guns, &c., with intent to inflict grievous bodily harm." },
        { section: "Section 36", title: "Obstructing or assaulting a clergyman or other minister in the discharge of his duties." },
        { section: "Section 38", title: "Assault with intent to commit felony, or on peace officers, &c." },
        { section: "Section 39", title: "Assaults with intent to obstruct the sale of grain, or its free passage." },
        { section: "Section 40", title: "Assaults on seamen, &c." },
        { section: "Section 41", title: "Assaults" },
        { section: "Section 42", title: "Persons committing any common assault or battery may be imprisoned or compelled by two magistrates to pay fine and costs not exceeding 5 l." },
        { section: "Section 43", title: "Persons convicted of aggravated assaults on females and boys under fourteen years of age may be imprisoned or fined." },
        { section: "Section 47", title: "Assault occasioning bodily harm." },
        { section: "Section 56", title: "Child-stealing." },
      ]
    },
    {
      act: "Offensive Weapons Act 2019",
      sections: [
        { section: "Section 1",  title: "Sale of corrosive products to persons under 18." },
        { section: "Section 6",  title: "Offence of having a corrosive substance in a public place." },
        { section: "Section 14", title: "Knife crime prevention order made otherwise than on conviction." },
        { section: "Section 19", title: "Knife crime prevention order made on conviction." },
        { section: "Section 34", title: "Sale etc of bladed articles to persons under 18." },
        { section: "Section 39", title: "Delivery of bladed products to persons under 18." },
        { section: "Section 44", title: "Prohibition on the possession of certain dangerous knives." },
        { section: "Section 45", title: "Prohibition on the possession of offensive weapons on further education premises." },
        { section: "Section 46", title: "Prohibition on the possession of offensive weapons." },
        { section: "Section 50", title: "Offence of threatening with offensive weapon etc in a public place etc." },
        { section: "Section 51", title: "Offence of threatening with offensive weapon etc on further education premises." },
        { section: "Section 52", title: "Offence of threatening with an offensive weapon etc in a private place." },
        { section: "Section 54", title: "Prohibition of certain firearms etc." },
      ]
    },
    {
      act: "Criminal Damage Act 1971",
      sections: [
        { section: "Section 1", title: "Destroying or damaging property." },
        { section: "Section 2", title: "Threats to destroy or damage property." },
        { section: "Section 3", title: "Possessing anything with intent to destroy or damage property." },
        { section: "Section 6", title: "Search for things intended for use in committing offences of criminal damage." },
        { section: "Section 9", title: "Evidence in connection with offences under this Act." },
      ]
    },
    {
      act: "Police Reform Act 2002",
      sections: [
        { section: "Section 54", title: "Anti-social behaviour orders." },
        { section: "Section 56", title: "Specimens taken from persons incapable of consenting." },
        { section: "Section 57", title: "Use of specimens taken from persons incapable of consenting." },
        { section: "Section 58", title: "Equivalent provision for offences connected with transport systems." },
        { section: "Section 59", title: "Vehicles used in manner causing alarm, distress or annoyance." },
        { section: "Section 60", title: "Retention etc. of vehicles seized under section 59." },
        { section: "Section 61", title: "Anti-social behaviour orders." },
        { section: "Section 67", title: "Sex offenders: England and Wales." },
        { section: "Section 68", title: "Interim orders for sex offenders: England and Wales." },
      ]
    },
    {
      act: "Firearms Act 1968",
      sections: [
        { section: "Section 1",  title: "Requirement of firearm certificate." },
        { section: "Section 2",  title: "Requirement of certificate for possession of shot guns." },
        { section: "Section 3",  title: "Business and other transactions with firearms and ammunition." },
        { section: "Section 5",  title: "Weapons subject to general prohibition." },
        { section: "Section 6",  title: "Power to prohibit movement of arms and ammunition." },
        { section: "Section 7",  title: "Police permit." },
        { section: "Section 8",  title: "Authorised dealing with firearms." },
        { section: "Section 10", title: "Slaughter of animals." },
        { section: "Section 16", title: "Possession of firearm with intent to injure." },
        { section: "Section 16A", title: "Possession of firearm with intent to cause fear of violence." },
        { section: "Section 17", title: "Use of firearm to resist arrest." },
        { section: "Section 18", title: "Carrying firearm with criminal intent." },
        { section: "Section 19", title: "Carrying firearm in a public place." },
        { section: "Section 19A", title: "Having small-calibre pistol outside premises of licensed pistol club." },
        { section: "Section 20", title: "Trespassing with firearm." },
        { section: "Section 21", title: "Possession of firearms by persons previously convicted of crime." },
        { section: "Section 21A", title: "Firing an air weapon beyond premises." },
        { section: "Section 22", title: "Acquisition and possession of firearms by minors." },
        { section: "Section 24", title: "Supplying firearms to minors." },
        { section: "Section 24ZA", title: "Failing to prevent minors from having air weapons." },
        { section: "Section 24A", title: "Supplying imitation firearms to minors." },
        { section: "Section 25", title: "Supplying firearm to person drunk or insane." },
        { section: "Section 30", title: "Revocation of certificates." },
        { section: "Section 31", title: "Certificate for prohibited weapon." },
        { section: "Section 32", title: "Certificate for prohibited weapon." },
        { section: "Section 46", title: "Power of search with warrant." },
        { section: "Section 47", title: "Powers of constables to stop and search." },
        { section: "Section 48", title: "Production of certificates." },
        { section: "Section 57", title: "Exception for airsoft guns." },
      ]
    },
    {
      act: "Fire and Rescue Services Act 2004",
      sections: [
        { section: "Section 37", title: "Prohibition on employment of police in fire-fighting." },
        { section: "Section 38", title: "Duty to secure water supply etc." },
        { section: "Section 39", title: "Supply of water by water undertakers." },
        { section: "Section 40", title: "Emergency supply by water undertaker." },
        { section: "Section 41", title: "Supply by other persons." },
        { section: "Section 42", title: "Fire hydrants." },
        { section: "Section 43", title: "Notice of works affecting water supply and fire hydrants." },
        { section: "Section 44", title: "Powers of fire-fighters etc in an emergency etc." },
      ]
    },
    {
      act: "Criminal Justice Act 1988",
      sections: [
        { section: "Section 139", title: "Offence of having article with blade or point in public place." },
        { section: "Section 139AA", title: "Offence of threatening with article with blade or point or offensive weapon" },
        { section: "Section 139B", title: "Power of entry to search for articles with a blade or point and offensive weapons." },
      ]
    },
    {
      act: "Terrorism Act 2000",
      sections: [
        { section: "Section 43", title: "Search of persons." },
        { section: "Section 43A", title: "Search of vehicles" },
        { section: "Section 81", title: "Arrest of suspected terrorists: power of entry." },
        { section: "Section 82", title: "Arrest and seizure: constables." },
        { section: "Section 116", title: "Powers to stop and search." },
      ]
    },
    {
      act: "Malicious Communications Act 1988",
      sections: [
        { section: "Section 1", title: "Offence of sending letters etc. with intent to cause distress or anxiety." },
      ]
    },
    {
      act: "Theft Act 1968",
      sections: [
        { section: "Section 7",  title: "Theft." },
        { section: "Section 8",  title: "Robbery." },
        { section: "Section 9",  title: "Burglary." },
        { section: "Section 10", title: "Aggravated burglary." },
        { section: "Section 11", title: "Removal of articles from places open to the public." },
        { section: "Section 12", title: "Taking motor vehicle or other conveyance without authority." },
        { section: "Section 12A", title: "Aggravated vehicle-taking." },
        { section: "Section 21", title: "Blackmail." },
        { section: "Section 22", title: "Handling stolen goods." },
        { section: "Section 25", title: "Going equipped for stealing, etc." },
        { section: "Section 26", title: "Search for stolen goods." },
        { section: "Section 27", title: "Evidence and procedure on charge of theft or handling stolen goods." },
      ]
    },
    {
      act: "Police Act 1996",
      sections: [
        { section: "Section 89", title: "Assaults on constables." },
        { section: "Section 89(2)", title: "Resisting or wilfully obstructing a constable in the execution of his duty" },
        { section: "Section 90", title: "Impersonation," },
      ]
    },
    {
      act: "Criminal Attempts Act 1981",
      sections: [
        { section: "Section 1", title: "Attempting to commit an offence." },
        { section: "Section 3", title: "Offences of attempt under other enactments." },
        { section: "Section 8", title: "Abolition of offence of loitering etc. with intent." },
        { section: "Section 9", title: "Interference with vehicles." },
      ]
    },
    {
      act: "Anti-social Behaviour, Crime and Policing Act 2014",
      sections: [
        { section: "Section 1", title: "Power to grant injunctions." },
        { section: "Section 4", title: "Power of arrest." },
        { section: "Section 9", title: "Arrest without warrant." },
        { section: "Section 10", title: "Issue of arrest warrant." },
        { section: "Section 13", title: "Power to exclude person from home in cases of violence or risk of harm." },
        { section: "Section 22", title: "Power to make orders." },
        { section: "Section 30", title: "Breach of order." },
        { section: "Section 34", title: "Authorisations to use powers under section 35." },
        { section: "Section 35", title: "Directions excluding a person from an area." },
        { section: "Section 36", title: "Restrictions." },
        { section: "Section 37", title: "Surrender of property." },
        { section: "Section 38", title: "Record-keeping." },
        { section: "Section 39", title: "Offences." },
        { section: "Section 43", title: "Power to issue notices." },
        { section: "Section 44", title: "Occupiers of premises etc." },
        { section: "Section 45", title: "Occupier or owner unascertainable." },
        { section: "Section 46", title: "Appeals against notices." },
        { section: "Section 48", title: "Offence of failing to comply with notice." },
        { section: "Section 51", title: "Seizure of item used in commission of offence." },
        { section: "Section 59", title: "Power to make orders." },
        { section: "Section 63", title: "Consumption of alcohol in breach of prohibition in order." },
        { section: "Section 67", title: "Offence of failing to comply with order." },
        { section: "Section 76", title: "Power to issue closure notices." },
        { section: "Section 98", title: "Conduct causing nuisance to landlord etc." },
        { section: "Section 99", title: "Offences connected with riot." },
        { section: "Section 106", title: "Keeping dogs under proper control." },
        { section: "Section 147", title: "Powers to seize invalid passports etc." },
      ]
    },
    {
      act: "Criminal Law Act 1967",
      sections: [
        { section: "Section 2", title: "Arrest without warrant." },
        { section: "Section 3", title: "Use of force in making arrest." },
        { section: "Section 4", title: "Penalties for assisting offenders." },
        { section: "Section 5", title: "Penalties for concealing offences or giving false information." },
      ]
    },
    {
      act: "Dangerous Dogs Act 1991",
      sections: [
        { section: "Section 1", title: "Dogs bred for fighting." },
        { section: "Section 3", title: "Keeping dogs under proper control." },
        { section: "Section 5", title: "Seizure, entry of premises and evidence." },
        { section: "Section 6", title: "Dogs owned by young persons." },
        { section: "Section 7", title: "Muzzling and leads." },
      ]
    },
    {
      act: "Forgery and Counterfeiting Act 1981",
      sections: [
        { section: "Section 1", title: "Offence of forgery." },
        { section: "Section 2", title: "Offence of copying a false instrument." },
        { section: "Section 3", title: "Offence of using a false instrument." },
        { section: "Section 4", title: "Offence of using a copy of a false instrument." },
        { section: "Section 14", title: "Offences of counterfeiting notes and coins." },
        { section: "Section 15", title: "Offences of passing etc. counterfeit notes and coins." },
        { section: "Section 16", title: "Offences involving the custody or control of counterfeit notes and coins." },
        { section: "Section 17", title: "Offences involving the making or custody or control of counterfeiting materials and implements." },
        { section: "Section 18", title: "Offence of reproducing British currency notes." },
        { section: "Section 19", title: "Offences of making etc. imitation British coins." },
        { section: "Section 20", title: "Prohibition of importation of counterfeit notes and coins." },
        { section: "Section 21", title: "Prohibition of exportation of counterfeit notes and coins." },
      ]
    },
    {
      act: "Fraud Act 2006",
      sections: [
        { section: "Section 1", title: "Fraud." },
        { section: "Section 2", title: "Fraud by false representation." },
        { section: "Section 3", title: "Fraud by failing to disclose information." },
        { section: "Section 4", title: "Fraud by abuse of position." },
        { section: "Section 6", title: "Possession etc. of articles for use in frauds." },
        { section: "Section 7", title: "Making or supplying articles for use in frauds." },
        { section: "Section 9", title: "Participating in fraudulent business carried on by sole trader etc." },
      ]
    },
    {
      act: "Bribery Act 2010",
      sections: [
        { section: "Section 1", title: "Offences of bribing another person." },
        { section: "Section 2", title: "Offences relating to being bribed" },
        { section: "Section 3", title: "Function or activity to which bribe relates." },
        { section: "Section 4", title: "Improper performance to which bribe relates." },
        { section: "Section 6", title: "Bribery of foreign public officials." },
        { section: "Section 7", title: "Failure of commercial organisations to prevent bribery." },
      ]
    },
    {
      act: "Online Safety Act 2023",
      sections: [
        { section: "Section 179", title: "False communications offence." },
        { section: "Section 181", title: "Threatening communications offence." },
        { section: "Section 183", title: "Offences of sending or showing flashing images electronically." },
        { section: "Section 184", title: "Offence of encouraging or assisting serious self-harm." },
      ]
    },
    {
      act: "Mental Capacity Act 2005",
      sections: [
        { section: "Section 5", title: "Acts in connection with care or treatment" },
        { section: "Section 6", title: "Limitations - Use of force" },
        { section: "Section 44", title: "Treatment or Neglect" },
      ]
    },
    {
      act: "Football (Offences) Act 1991",
      sections: [
        { section: "Section 1", title: "Designated football matches." },
        { section: "Section 2", title: "Throwing of missiles." },
        { section: "Section 3", title: "Indecent or racialist chanting." },
        { section: "Section 4", title: "Going onto the playing area." },
      ]
    },
    {
      act: "Regulation of Investigatory Powers Act 2000",
      sections: [
        { section: "Section 1", title: "Unlawful interception." },
        { section: "Section 3", title: "Lawful interception without an interception warrant." },
        { section: "Section 4", title: "Power to provide for lawful interception." },
        { section: "Section 5", title: "Interception with a warrant." },
        { section: "Section 6", title: "Application for issue of an interception warrant." },
        { section: "Section 7", title: "Issue of warrants." },
        { section: "Section 19", title: "Offence for unauthorised disclosures." },
        { section: "Section 27", title: "Lawful surveillance etc." },
        { section: "Section 28", title: "Authorisation of directed surveillance." },
        { section: "Section 29", title: "Authorisation of covert human intelligence sources." },
        { section: "Section 29A", title: "Section 29: supplementary provision in relation to relevant collaborative units." },
        { section: "Section 29B", title: "Covert human intelligence sources: criminal conduct authorisations." },
        { section: "Section 29C", title: "Criminal conduct authorisations: safeguards for juveniles." },
        { section: "Section 29D", title: "Criminal conduct authorisations: safeguards for vulnerable adults." },
        { section: "Section 32", title: "Authorisation of intrusive surveillance." },
        { section: "Section 53", title: "Failure to comply with a notice." },
        { section: "Section 54", title: "Tipping-off." },
      ]
    },
    {
      act: "Prevention of Crime Act 1953",
      sections: [
        { section: "Section 1", title: "Prohibition of the carrying of offensive weapons without lawful authority or reasonable excuse." },
        { section: "Section 1A", title: "Offence of threatening with offensive weapon in public." },
      ]
    },
    {
      act: "Computer Misuse Act 1990",
      sections: [
        { section: "Section 1", title: "Unauthorised access to computer material." },
        { section: "Section 2", title: "Unauthorised access with intent to commit or facilitate commission of further offences." },
        { section: "Section 3", title: "Unauthorised acts with intent to impair, or with recklessness as to impairing, operation of computer, etc." },
        { section: "Section 3ZA", title: "Unauthorised acts causing, or creating risk of, serious damage." },
        { section: "Section 3A", title: "Making, supplying or obtaining articles for use in offence under section 1, 3 or 3ZA." },
      ]
    },
    {
      act: "Animal Welfare Act 2006",
      sections: [
        { section: "Section 2", title: "”Protected Animals.”" },
        { section: "Section 3", title: "Responsibility for animals." },
        { section: "Section 4", title: "Unnecessary suffering." },
        { section: "Section 6", title: "Docking of dogs' tails." },
        { section: "Section 7", title: "Administration of poisons etc." },
        { section: "Section 8", title: "Fighting etc." },
        { section: "Section 9", title: "Duty of person responsible for animal to ensure welfare." },
        { section: "Section 13", title: "Licensing or registration of activities involving animals." },
        { section: "Section 18", title: "Powers in relation to animals in distress." },
        { section: "Section 19", title: "Power of entry for section 18 purposes." },
        { section: "Section 20", title: "Orders in relation to animals taken under section 18(5)." },
        { section: "Section 22", title: "Seizure of animals involved in fighting offences." },
        { section: "Section 23", title: "Entry and search under warrant in connection with offences." },
        { section: "Section 24", title: "Entry for purposes of arrest" },
        { section: "Section 30", title: "Power of local authority to prosecute offences." },
        { section: "Section 32", title: "Imprisonment or fine." },
        { section: "Section 35", title: "Seizure of animals in connection with disqualification." },
      ]
    },
  ];

  // ---------- HELPERS ----------
  const $ = (sel, root=document) => root.querySelector(sel);
  const $$ = (sel, root=document) => Array.from(root.querySelectorAll(sel));

  function norm(s){ return (s||"").toLowerCase().trim(); }

  function copyText(text){
    navigator.clipboard.writeText(text).then(()=>{
      toast(`Copied: ${text}`);
    }).catch(()=>{
      toast("Copy failed (clipboard blocked). You can select & copy manually.");
    });
  }

  let toastTimer = null;
  function toast(msg){
    let el = $("#toast");
    if(!el){
      el = document.createElement("div");
      el.id = "toast";
      el.style.position = "fixed";
      el.style.left = "50%";
      el.style.bottom = "18px";
      el.style.transform = "translateX(-50%)";
      el.style.padding = "10px 12px";
      el.style.border = "1px solid rgba(38,48,67,.9)";
      el.style.background = "rgba(17,24,39,.92)";
      el.style.backdropFilter = "blur(10px)";
      el.style.borderRadius = "12px";
      el.style.color = "var(--text)";
      el.style.fontSize = "13px";
      el.style.zIndex = "999";
      el.style.maxWidth = "min(560px, calc(100vw - 24px))";
      el.style.boxShadow = "0 10px 30px rgba(0,0,0,.25)";
      document.body.appendChild(el);
    }
    el.textContent = msg;
    el.style.display = "block";
    clearTimeout(toastTimer);
    toastTimer = setTimeout(()=>{ el.style.display="none"; }, 2200);
  }

  // ---------- STATE ----------
  const state = {
    q: "",
    actFilter: new Set(), // act names
  };

  // ---------- UI BUILD ----------
  function buildChips(){
    const chips = $("#chips");
    chips.innerHTML = "";

    const all = document.createElement("span");
    all.className = "chip";
    all.textContent = "All Acts";
    all.setAttribute("role","button");
    all.setAttribute("tabindex","0");
    all.setAttribute("aria-pressed","true");
    all.addEventListener("click", ()=>{ state.actFilter.clear(); render(); });
    chips.appendChild(all);

    acts.forEach(a=>{
      const chip = document.createElement("span");
      chip.className = "chip";
      chip.textContent = a.act;
      chip.setAttribute("role","button");
      chip.setAttribute("tabindex","0");
      chip.setAttribute("aria-pressed","false");
      chip.addEventListener("click", ()=>{
        if(state.actFilter.has(a.act)) state.actFilter.delete(a.act);
        else state.actFilter.add(a.act);
        render();
      });
      chips.appendChild(chip);
    });
  }

  function updateChips(){
    const chipEls = $$(".chip", $("#chips"));
    chipEls.forEach((c, idx)=>{
      if(idx === 0){
        const pressed = state.actFilter.size === 0;
        c.setAttribute("aria-pressed", String(pressed));
      }else{
        const actName = c.textContent;
        c.setAttribute("aria-pressed", String(state.actFilter.has(actName)));
      }
    });
  }

  function matches(sectionObj, actName, q){
    if(!q) return true;
    const hay = norm(`${actName} ${sectionObj.section} ${sectionObj.title}`);
    return hay.includes(q);
  }

  function filteredActs(){
    const q = norm(state.q);
    const actSet = state.actFilter;

    return acts
      .filter(a => actSet.size === 0 || actSet.has(a.act))
      .map(a=>{
        const secs = a.sections.filter(s => matches(s, a.act, q));
        return { act: a.act, sections: secs };
      })
      .filter(a => a.sections.length > 0);
  }

  function render(){
    updateChips();

    const data = filteredActs();
    const grid = $("#grid");
    grid.innerHTML = "";

    const totalActs = acts.length;
    const totalSections = acts.reduce((n,a)=>n+a.sections.length,0);

    const shownActs = data.length;
    const shownSections = data.reduce((n,a)=>n+a.sections.length,0);

    $("#resultsMeta").textContent =
      `Showing ${shownSections} / ${totalSections} sections across ${shownActs} / ${totalActs} Acts.`;

    $("#empty").style.display = shownSections === 0 ? "block" : "none";

    data.forEach(a=>{
      const card = document.createElement("article");
      card.className = "card";

      const head = document.createElement("header");
      const row = document.createElement("div");
      row.className = "act";

      const h2 = document.createElement("h2");
      h2.textContent = a.act;

      const count = document.createElement("div");
      count.className = "count";
      count.textContent = `${a.sections.length} section${a.sections.length===1?"":"s"}`;

      row.appendChild(h2);
      row.appendChild(count);
      head.appendChild(row);

      const list = document.createElement("div");
      list.className = "list";

      a.sections.forEach(s=>{
        const d = document.createElement("details");

        const sum = document.createElement("summary");
        const left = document.createElement("div");
        left.style.display="flex";
        left.style.flexWrap="wrap";
        left.style.gap="6px";
        left.style.alignItems="baseline";

        const sec = document.createElement("span");
        sec.className = "sec";
        sec.textContent = s.section;

        const desc = document.createElement("span");
        desc.className = "desc";
        desc.textContent = s.title;

        left.appendChild(sec);
        left.appendChild(desc);

        const caret = document.createElement("span");
        caret.setAttribute("aria-hidden","true");
        caret.textContent = "▾";
        caret.style.color = "var(--muted)";

        sum.appendChild(left);
        sum.appendChild(caret);

        const mono = document.createElement("div");
        mono.className = "mono";
        const ref = `${a.act} — ${s.section}: ${s.title}`;
        mono.textContent = ref;

        const copyRow = document.createElement("div");
        copyRow.className = "copyRow";

        const b1 = document.createElement("button");
        b1.type = "button";
        b1.className = "mini";
        b1.textContent = "Copy full reference";
        b1.addEventListener("click", ()=>copyText(ref));

        const b2 = document.createElement("button");
        b2.type = "button";
        b2.className = "mini";
        b2.textContent = "Copy Act + section";
        b2.addEventListener("click", ()=>copyText(`${a.act} — ${s.section}`));

        const b3 = document.createElement("button");
        b3.type = "button";
        b3.className = "mini";
        b3.textContent = "Copy section title";
        b3.addEventListener("click", ()=>copyText(s.title));

        copyRow.append(b1,b2,b3);

        d.appendChild(sum);
        d.appendChild(copyRow);
        d.appendChild(mono);
        list.appendChild(d);
      });

      card.appendChild(head);
      card.appendChild(list);
      grid.appendChild(card);
    });
  }

  // ---------- EVENTS ----------
  buildChips();
  render();

  $("#q").addEventListener("input", (e)=>{
    state.q = e.target.value;
    render();
  });

  $("#clear").addEventListener("click", ()=>{
    state.q = "";
    state.actFilter.clear();
    $("#q").value = "";
    render();
  });

  $("#expandAll").addEventListener("click", ()=>{
    $$("details").forEach(d=>d.open = true);
  });

  $("#collapseAll").addEventListener("click", ()=>{
    $$("details").forEach(d=>d.open = false);
  });

  // keyboard toggle for chips
  $("#chips").addEventListener("keydown", (e)=>{
    if(e.key !== "Enter" && e.key !== " ") return;
    const t = e.target;
    if(t.classList.contains("chip")){ e.preventDefault(); t.click(); }
  });
</script>
</body>
</html>
