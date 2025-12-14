# SlotMachine
 SlotMachine js puro 


class SlotMachine {

 constructor() {
   this.symbols = ['🎰', '🍒', '💎', '🎲'];
   this.animationInterval = null;

   this.playerBalancer  = 50;
   this.spinConst = 5;

    this.scoreRules ={
    WinPontos: 10,
    PairPontos: 5,
    }

   }
   updateBalance(score) {
    this.playerBalancer += score;
   }

   calcularScore(result){
    let score = 0;

    if(this.checkWin(result)){
        score = this.scoreRules.WinPontos;
    }
   else if(this.checkPair(result)){
      score = this.scoreRules.PairPontos;
   }
   return score; 
   }

   

   

  startSpinAnimation() {

  if(this.animationInterval) return;
  this.animationInterval = setInterval(() => {
    console.clear();

    const x1 =  this.getRandomSymbol();
    const x2 =  this.getRandomSymbol();
    const x3 =  this.getRandomSymbol();

    console.log(`| ${x1} | ${x2} | ${x3} |`);
    console.log("-- Girando... --");

 }, 100);
}
 stopSpinAnimation() {
    if(this.animationInterval){
        clearInterval(this.animationInterval);
    this.animationInterval = null;
    }
    console.clear();
 }

 spin() {

    if(this.playerBalancer < this.spinConst){
        console.log(`❌ SALDO INSUFICIENTE. Você precisa de ${this.spinCost} para jogar. Saldo atual: ${this.playerBalance}`);
        console.log(" RECAREGUE O SALDO PARA JOGAR");
        return;
    }
    // 2. Deduzir o custo da jogada
        this.playerBalancer -= this.spinCost; 
        console.log(`CUSTO: -${this.spinCost}. SALDO ATUAL: ${this.playerBalance}`);
        console.log("GIRANDO AS ROLETAS...");
   
    console.log("GIRANDO AS ROLETAS...");

    this.startSpinAnimation();

    
    setTimeout(() => {
        this.stopSpinAnimation();
     
    const reel1 = this.getRandomSymbol();
    const reel2 = this.getRandomSymbol();
    const reel3 = this.getRandomSymbol(); 
    const result = [reel1, reel2, reel3]
    const finalScore = this.calcularScore(result);
    console.log(`\n🎰Resultado final🎰:`);
    console.log(`| ${reel1} | ${reel2} | ${reel3} |`);
    console.log(this.getMensage(result));
    console.log(`✨ Pontos Ganhos: ${finalScore} ✨`);
    console.log("-----PRESIONE ENTER PARA JOGAR NOVAMENTE-----");
    }, 2000);

 }
    getRandomSymbol() {
        const randomIndex = Math.floor(Math.random() * this.symbols.length);
        return this.symbols[randomIndex];
    }

    checkWin(result) {
        return result [0] === result [1] && result [1] === result [2];
    }
     checkPair(result) {
          return (
        (result [0] === result [1] && result [1] !== result [2]) ||
        (result [0] === result [2] && result [1] !== result [0]) ||
        (result [1] === result [2] && result [0] !== result [1])
          ); 
    
    }
        getMensage(result) {

            if (this.checkWin(result)) {
                return "Parabéns! Você ganhou!";
            } else if (this.checkPair(result))  {
                  return "Quase lá! Tente novamente.";
            } else {
                return "Boa tentativa! Continue jogando.";
            }
      
            
        }
     }



            const  slot  = new SlotMachine();
            slot.spin();

 

     
    










