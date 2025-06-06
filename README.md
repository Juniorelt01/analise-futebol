# Atualizar HTML com campo de busca funcional (filtro por nome do time, dados simulados)

html_with_search = html_20_jogos.replace(
    '<input type="text" id="buscarJogo" placeholder="Digite o nome dos times">',
    '<input type="text" id="buscarJogo" placeholder="Digite o nome do time" onkeyup="filtrarTime()">'
)

# Adicionar script para simular busca por nome do time
search_script = """
<script>
  function filtrarTime() {
    const input = document.getElementById('buscarJogo').value.toLowerCase();
    const info = document.getElementById('infoJogo');
    const titulo = info.querySelector('h2').textContent.toLowerCase();
    if (input === '') {
      info.style.display = 'block';
      return;
    }
    if (titulo.includes(input)) {
      info.style.display = 'block';
    } else {
      info.style.display = 'none';
    }
  }
</script>
</body>
</html>
"""

html_with_search = html_with_search.replace("</body>\n</html>", search_script)

# Salvar versão com campo de busca funcional
search_path = Path("/mnt/data/site_com_busca_por_time.html")
search_path.write_text(html_with_search, encoding="utf-8")

# Também zipar para facilitar envio
search_zip = "/mnt/data/site_com_busca_por_time.zip"
with zipfile.ZipFile(search_zip, 'w') as zipf:
    zipf.write(search_path, arcname="index.html")

search_zip
