# PC Agent-E

<p align="center">
  📄 <a href="https://arxiv.org/abs/2505.13909" target="_blank">Paper</a> &nbsp; | &nbsp;
  🌐 <a href="https://gair-nlp.github.io/PC-Agent-E" target="_blank">Website</a> &nbsp; | &nbsp;
  🤖 <a href="https://huggingface.co/henryhe0123/PC-Agent-E" target="_blank">Model</a> &nbsp; | &nbsp;
  🤗 <a href="https://huggingface.co/datasets/henryhe0123/PC-Agent-E" target="_blank">Dataset</a>
</p>

<p align="center">
  <img src="./assets/first_image.png" width="50%" alt="Animação do PC Agent-E">
</p>

## Visão Geral

O PC Agent-E é um framework eficiente de treinamento de agentes para automação de uso de computador, que extrai fortes capacidades com eficiência de dados notável. A implementação possui quatro componentes principais:

1. **Coleta de Trajetórias**: Coleta trajetórias de tarefas de anotadores humanos usando [PC Tracker](https://github.com/GAIR-NLP/PC-Agent?tab=readme-ov-file#pc-tracker)
2. **Completação de Pensamentos**: Reconstrói o processo mental humano latente precedente a cada ação
3. **Impulso de Trajetória**: Sintetiza decisões de ação alternativas diversificadas
4. **Treinamento de Agente**: Treina o modelo nativo de agente usando trajetórias aumentadas

![Visão Geral do Framework](./assets/overview.png)

## Resultados Principais

Desempenho no benchmark WindowsAgentArena-V2 (Taxa de Sucesso %):

| Modelo | LibreOffice | Chrome | Edge | Sistema | VS Code | VLC | Utilitários | Total |
|--------|-------------|--------|------|---------|---------|-----|-------------|-------|
| Qwen2.5-VL-72B | 0.0 | 34.7 | 15.4 | 20.8 | 26.3 | 7.6 | 16.7 | 14.9 |
| UI-TARS-1.5-7B | **7.1** | 34.7 | 23.1 | 45.8 | 21.1 | 7.6 | 16.7 | 21.3 |
| UI-TARS-72B-DPO | 0.0 | 40.6 | 38.5 | 58.3 | 36.8 | 7.6 | 25.0 | 26.2 |
| Claude 3.7 Sonnet | 2.4 | 46.5 | **61.5** | 54.2 | 52.6 | 29.0 | 16.7 | 32.6 |
| Claude 3.7 Sonnet (thinking) | 2.4 | **64.1** | 46.2 | **66.7** | 52.6 | 21.9 | 25.0 | 35.4 |
| **PC Agent-E (Nossa)** | 4.8 | **64.1** | 46.2 | 50.0 | **57.9** | **35.7** | **33.3** | **36.0** |

## Demonstrações

Veja o PC Agent-E controlando um computador autonomamente para completar tarefas em sistemas Windows e Linux.

[![Vídeo Demo 1](https://github.com/user-attachments/assets/9540d8cb-630d-41e2-a108-a96ca3fcb32e)](https://github.com/user-attachments/assets/9540d8cb-630d-41e2-a108-a96ca3fcb32e)

[![Vídeo Demo 2](https://github.com/user-attachments/assets/18b436e7-733f-49a5-8716-25c29a990766)](https://github.com/user-attachments/assets/18b436e7-733f-49a5-8716-25c29a990766)

## Início Rápido

### 1. Coleta de Trajetórias

Colete trajetórias brutas usando PC Tracker. Consulte a [documentação do PC Tracker](https://github.com/GAIR-NLP/PC-Agent?tab=readme-ov-file#pc-tracker) para instruções de uso.

### 2. Pós-processamento

Converta trajetórias brutas em dados de alta qualidade para treinamento:

1. Coloque os dados gravados no diretório `data/`
2. Execute o pipeline de pós-processamento:
   bash
   python scripts/postprocess.py --input data/raw --output data/processed
   

### 3. Completação de Pensamentos

Reconstrua o raciocínio humano por trás das ações:

bash
python scripts/thought_completion.py --data data/processed


### 4. Impulso de Trajetória

Gere alternativas de ação diversificadas:

bash
python scripts/trajectory_boost.py --data data/processed --boost-factor 3


### 5. Treinamento do Modelo

Treine o agente com as trajetórias aumentadas:

bash
python train.py --config configs/pc_agent_e.yaml --data data/augmented


## Instalação

### Pré-requisitos

- Python 3.10+
- PyTorch 2.0+
- CUDA 11.8+ (se usando GPU)

### Configuração

bash
# Clone o repositório
git clone https://github.com/GAIR-NLP/PC-Agent-E.git
cd PC-Agent-E

# Crie ambiente virtual
python -m venv pc_agent_env
source pc_agent_env/bin/activate  # Linux/Mac
# pc_agent_env\Scripts\activate  # Windows

# Instale dependências
pip install -r requirements.txt


## Arquitetura

O framework segue um pipeline sistemático:

1. **Camada de Coleta de Dados**: Captura interações humano-computador via PC Tracker
2. **Camada de Processamento**: Enriquece trajetórias com completação de pensamentos e impulso
3. **Camada de Treinamento**: Supervisiona o modelo no dataset aumentado
4. **Camada de Inferência**: Executa ações em ambientes do mundo real

## Citação

bibtex
@article{he2025pcagent_e,
  title={Efficient Agent Training for Computer Use},
  author={He, Henry and others},
  journal={arXiv preprint arXiv:2505.13909},
  year={2025}
}


## Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

## Contribuindo

Contribuições são bem-vindas! Por favor, leia nossas [Diretrizes de Contribuição](CONTRIBUTING.md) antes de enviar um pull request.

## Dúvidas?

Para questões técnicas, por favor abra uma issue no GitHub. Para questões de pesquisa, contate os autores via o artigo.