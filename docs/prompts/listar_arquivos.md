Get-ChildItem -Recurse -File |
Where-Object {
    $_.FullName -notmatch '\\(node_modules|\.git|\.vercel|\.astro|dist)\\'
} |
Select-Object -ExpandProperty FullName > estrutura-projeto.txt