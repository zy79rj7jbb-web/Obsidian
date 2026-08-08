

```dataviewjs
const start = moment(dv.current().week_start);
const end = start.clone().add(3,"days");

const pages = dv.pages('"Report"')
.where(p => {
    const date = moment(p.file.name,"YYYY-MM-DD");
    return date.isBetween(start,end,null,"[]");
});


function sum(field){

return pages
.array()
.map(p => Number(p[field] ?? 0))
.reduce((a,b)=>a+b,0);

}


function progress(value, goal){

const percent = Math.round((value / goal) * 100);

let color;

if(percent >= 100){
    color="🟢";
}
else if(percent >= 70){
    color="🟡";
}
else{
    color="🔴";
}


const blocks = Math.min(
    10,
    Math.round(percent / 10)
);

return `
${"█".repeat(blocks)}
${"░".repeat(10-blocks)}
${percent}%
${color}
`;

}


const rows=[

[
"💻 Programming",
sum("Programming"),
dv.current().Programming_goal
],

[
"📖 Book",
sum("Book"),
dv.current().Book_goal
],

[
"🇬🇧 English",
sum("English"),
dv.current().English_goal
],

[
"💾 Obsidian",
sum("Obsidian"),
dv.current().Obsidian_goal
],

[
"😴 Sleep",
sum("Sleep"),
dv.current().Sleep_goal
],

[
"🚶 Distance",
sum("Distance"),
dv.current().Distance_goal
]

];


dv.table(
[
"Категория",
"Факт",
"План",
"Прогресс"
],

rows.map(r=>[
r[0],
r[1],
r[2],
progress(r[1],r[2])
])

);
```
