---
name: vehicle-colors-api
description: API estática em JSON que fornece o mapeamento de nomes de cores automotivas em português para seus respectivos códigos Hexadecimais. Pode ser consumida por sistemas frontend como o Lovable ou Glide.
license: Complete terms in LICENSE.txt
---

# Vehicle Colors API Skill

Esta skill atua como um simulador de banco de dados/API para cores automotivas padrão da indústria. Ela fornece um catálogo mapeando os nomes comerciais das cores em português para códigos Hexadecimais, divididos em categorias como Cores Sólidas, Metálicas e Perolizadas.

## Estrutura de Arquivos
- `colors.json`: O banco de dados completo contendo o mapeamento das cores.

## Como Consumir (Para Desenvolvedores Frontend / Lovable / FlutterFlow)

Para acessar estas cores em tempo real no seu sistema, você deve fazer uma requisição HTTP `GET` para o link Raw deste arquivo no GitHub. 

### Exemplo em JavaScript (Fetch API)

```javascript
// URL Raw do GitHub onde o colors.json está hospedado
const GIT_RAW_URL = "https://raw.githubusercontent.com/SEU_USUARIO/SEU_REPOSITORIO/main/colors.json";

async function buscarCoresAutomotivas() {
  try {
    const response = await fetch(GIT_RAW_URL);
    const data = await response.json();
    console.log("Banco de cores carregado!", data);
    
    // Exemplo: Pegando a cor "Prata Geada" (que é uma cor metálica)
    const hexPrataGeada = data.cores_metalicas["Prata Geada"];
    console.log(`O Hex do Prata Geada é: ${hexPrataGeada}`);
    return data;
  } catch (error) {
    console.error("Erro ao buscar cores:", error);
  }
}
```

## Como Expandir a Base de Dados

Para adicionar novas cores ao sistema que consomem essa API:
1. Abra o arquivo `colors.json` contido no repositório.
2. Identifique o tipo de tinta correto (Sólida, Metálica ou Perolizada).
3. Adicione o nome da cor exatamente como consta no catálogo da montadora seguido do seu Hex correspondente. Exemplo: `"Azul Búzios": "#3A5F7D"`.
4. Faça o `commit` e `push` para a branch principal (`main`).
5. As plataformas conectadas (Lovable, etc) receberão os novos dados na próxima vez que a rotina de `fetch` rodar.
