from flask import Flask, render_template, request, jsonify

app = Flask(__name__)

# Dados fictícios de serviços para exemplo
servicos = [
    {"id": 1, "nome": "Atendimento Médico", "categoria": "Saúde", "local": "Recife", "descricao": "Consulta médica especializada"},
    {"id": 2, "nome": "Assistência Jurídica", "categoria": "Assistência Jurídica", "local": "Olinda", "descricao": "Apoio legal para mulheres"},
    {"id": 3, "nome": "Apoio Psicológico", "categoria": "Psicologia", "local": "Caruaru", "descricao": "Apoio psicológico gratuito"},
    {"id": 4, "nome": "Capacitação Profissional", "categoria": "Educação", "local": "Jaboatão", "descricao": "Cursos profissionalizantes"},
]

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/servicos')
def listar_servicos():
    categoria = request.args.get('categoria')
    if categoria:
        filtrados = [s for s in servicos if s['categoria'].lower() == categoria.lower()]
    else:
        filtrados = servicos
    return jsonify(filtrados)

@app.route('/servico/<int:servico_id>')
def detalhes_servico(servico_id):
    servico = next((s for s in servicos if s["id"] == servico_id), None)
    if servico:
        return jsonify(servico)
    else:
        return jsonify({"error": "Serviço não encontrado"}), 404

@app.route('/buscar', methods=['GET'])
def buscar_servico():
    termo = request.args.get('q')
    resultados = [s for s in servicos if termo.lower() in s['nome'].lower() or termo.lower() in s['descricao'].lower()]
    return jsonify(resultados)

if __name__ == '__main__':
    app.run(debug=True)
