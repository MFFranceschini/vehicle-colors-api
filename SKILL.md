---
name: vehicle-colors-api
description: API estática em JSON que fornece o mapeamento de nomes de cores automotivas em português para seus respectivos códigos Hexadecimais. Pode ser consumida por sistemas frontend como o Lovable ou Glide.
license: Complete terms in LICENSE.txt
---

# Vehicle Colors API Skill

Esta skill atua como um simulador de banco de dados/API para cores automotivas padrão da indústria. Ela fornece um catálogo mapeando os nomes comerciais das cores em português para códigos Hexadecimais, divididos em categorias como Cores Sólidas, Metálicas e Perolizadas.

## Estrutura de Arquivos Multi-idioma
- `colors-pt-br.json`: O banco de dados completo contendo o mapeamento das cores em Português do Brasil.
- `colors-eng.json`: A versão traduzida do banco de dados para sistemas em Inglês.

## Como Consumir (Para Desenvolvedores Frontend / Lovable / FlutterFlow)

Para acessar estas cores no seu sistema e garantir alta performance, faça uma requisição HTTP `GET` para o link Raw do arquivo correspondente no GitHub logo que a aplicação iniciar. Arquivos separados garantem que o usuário baixe apenas a linguagem que ele ou o sistema estão utilizando, economizando banda.

### Exemplo em JavaScript (Fetch API Multi-idioma)

```javascript
// URLs Raw do GitHub onde os arquivos estão hospedados (Ajuste o SEU_USUARIO/SEU_REPOSITORIO)
const API_URLS = {
  "pt-br": "https://raw.githubusercontent.com/SEU_USUARIO/vehicle-colors-api/main/colors-pt-br.json",
  "eng": "https://raw.githubusercontent.com/SEU_USUARIO/vehicle-colors-api/main/colors-eng.json"
};

async function fetchVehicleColors(userLanguage = 'pt-br') {
  // Define o link correto com base no idioma, usando pt-br como fallback seguro
  const url = API_URLS[userLanguage] || API_URLS["pt-br"];
  
  try {
    const response = await fetch(url);
    const data = await response.json();
    console.log(`Cores carregadas no idioma ${userLanguage}!`, data);
    return data;
  } catch (error) {
    console.error("Erro ao carregar a API de cores:", error);
  }
}

// Para usar na aplicação:
// const catalog = await fetchVehicleColors('eng');
// const colorHex = catalog.colors.metallic.examples["Sirius Silver (VW)"];
```

## Como Expandir a Base de Dados

Para adicionar novas cores ao sistema que consomem essa API:
1. Abra o arquivo `colors.json` contido no repositório.
2. Identifique o tipo de tinta correto (Sólida, Metálica ou Perolizada).
3. Adicione o nome da cor exatamente como consta no catálogo da montadora seguido do seu Hex correspondente. Exemplo: `"Azul Búzios": "#3A5F7D"`.
4. Faça o `commit` e `push` para a branch principal (`main`).
5. As plataformas conectadas (Lovable, etc) receberão os novos dados na próxima vez que a rotina de `fetch` rodar.
