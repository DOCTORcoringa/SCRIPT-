# Cores ANSI
green='\033[0;32m'
red='\033[0;31m'
pink='\033[1;35m'
reset='\033[0m'

# Nome do criador fixo
CRIA_NOME="Doctor Coringa Lunático"

# Bonequinho ASCII compacto
person_ascii=(
"  o  "
" /|\\ "
" / \\ "
)

# Perguntas para o usuário
read -p "Digite seu vulgo/nome: " VULGO

echo "Escolha a fonte para seu nome:"
echo "1) normal"
echo "2) slant (3D inclinado)"
echo "3) big"
echo "4) small"
read -p "Digite o número da opção (default 2): " fonte_opt

case $fonte_opt in
  1) fonte="standard" ;;
  2) fonte="slant" ;;
  3) fonte="big" ;;
  4) fonte="small" ;;
  *) fonte="slant" ;;
esac

echo "Escolha a cor:"
echo "1) Verde"
echo "2) Vermelho"
echo "3) Rosa"
read -p "Digite o número da cor (default 1): " cor_opt

case $cor_opt in
  1) cor=$green ;;
  2) cor=$red ;;
  3) cor=$pink ;;
  *) cor=$green ;;
esac

typing() {
    local text="$1"
    local len=${#text}
    for ((i=0; i<len; i++)); do
        echo -n "${text:i:1}"
        sleep 0.05
    done
    echo
}

clear

# Nome do criador no canto superior direito
echo -e "\033[1;50H${green}${CRIA_NOME}${reset}"

# Bonequinho no topo esquerdo
line=1
for i in "${person_ascii[@]}"; do
    echo -e "\033[${line};1H${green}${i}${reset}"
    ((line++))
done

# Mensagem digitada
echo -e "\033[5;1H${green}"
typing "Bem-vindo meu mestre, $VULGO"
echo -e "${reset}"

# Nome ASCII do usuário com fonte e cor escolhidos
figlet -f "$fonte" "$VULGO" | while IFS= read -r line; do
    echo -e "${cor}${line}${reset}"
done

