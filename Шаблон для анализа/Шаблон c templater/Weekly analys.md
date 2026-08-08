

```dataviewjs

dv.header(2,"🎯 Цели недели");

dv.table(
["Категория","Цель"],
[
["Programming",30],
["Programming Reading",7],
["Programming Coding",23],
["Book",7],
["English",5],
["Obsidian",3],
["Sleep",56],
["Distance",20]
]
);

```


# 📊 Dashboard недели


```dataviewjs
const start = dv.date("today").minus({ days: 7 });
const end = dv.date("today");

const pages = dv.pages('"Report"')
    .where(p => p.file.day)
    .where(p => p.file.day >= start && p.file.day <= end);

function number(value) {
    if (value == null) return 0;

    const match = String(value).match(/-?\d+([.,]\d+)?/);

    if (!match) return 0;

    return Number(match[0].replace(",", "."));
}

function sum(field) {
    let total = 0;

    for (const page of pages) {
        total += number(page[field]);
    }

    return Math.round(total * 100) / 100;
}

function avg(field) {
    if (pages.length === 0) return 0;

    return Math.round((sum(field) / pages.length) * 100) / 100;
}

dv.table(
["Категория","Итого","Среднее в день"],
[
["Programming",sum("Programming"),avg("Programming")],
["Programming Reading",sum("Programming Reading"),avg("Programming Reading")],
["Programming Coding",sum("Programming Coding"),avg("Programming Coding")],
["Ars",sum("Ars"),avg("Ars")],
["English",sum("English"),avg("English")],
["Book",sum("Book"),avg("Book")],
["Obsidian",sum("Obsidian"),avg("Obsidian")],
["Distance",sum("Distance"),avg("Distance")],
["Sleep",sum("Sleep"),avg("Sleep")],
["Games",sum("Games"),avg("Games")],
["Watching",sum("Watching"),avg("Watching")],
["Playing",sum("Playing"),avg("Playing")],
["Chill",sum("Chill"),avg("Chill")],
["Card",sum("Card"),avg("Card")]
]
);
```

---

# Самые важные показатели

```dataviewjs
const start = dv.date("today").minus({ days: 7 });
const end = dv.date("today");

const pages = dv.pages('"Report"')
.where(p => p.file.day)
.where(p => p.file.day >= start && p.file.day <= end);

function number(value){
    if(value == null) return 0;

    const match = String(value).match(/-?\d+([.,]\d+)?/);

    if(!match) return 0;

    return Number(match[0].replace(",","."));
}

function sum(field){
    let total = 0;

    for(const page of pages)
        total += number(page[field]);

    return Math.round(total*100)/100;
}

dv.paragraph(`
## 🎯 Programming: **${sum("Programming")} ч**

📚 Reading: **${sum("Programming Reading")} ч**

💻 Coding: **${sum("Programming Coding")} ч**

📖 Book: **${sum("Book")} ч**

🇬🇧 English: **${sum("English")} ч**

🚶 Distance: **${sum("Distance")} км**

😴 Sleep: **${sum("Sleep")} ч**
`);
```

---

# Графики

(сюда вставляешь все свои tracker-графики)
