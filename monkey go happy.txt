
var monkey , monkey_running , monkey_collided;

var ground;

var banana ,bananaImage, obstacle, obstacleImage;

var bananaGroup, obstacleGroup;

var survivalTime = 0;

var score = 0;

var end = 0;

var play = 1;

var gameState = play;

function preload(){
  
  
  
  monkey_running =            loadAnimation("sprite_0.png","sprite_1.png","sprite_2.png","sprite_3.png","sprite_4.png","sprite_5.png","sprite_6.png","sprite_7.png","sprite_8.png");
  
  monkey_collided = loadAnimation("sprite_0.png");
  
  bananaImage = loadImage("banana.png");
  obstacleImage = loadImage("obstacle.png");
 
}



function setup() {
  
  createCanvas(600,400);
  
  monkey = createSprite(110,395,0,0);
  monkey.addAnimation("running monkey",monkey_running);
  monkey.visible = false;
  monkey.scale = 0.14;
  
  ground = createSprite(300,395,600,10);
 
  bananaGroup = createGroup();
  obstacleGroup = createGroup();
  
}


function draw() {

background("black");
  
  monkey.collide(ground);
  
  stroke("yellow");
  textSize(20);
  fill("red")
  text("Score:"+score,80,50);
  
   stroke("yellow");
   textSize(20);
   fill("red");
   text("Survival-time:"+survivalTime,400,50);
  
  monkey.velocityY = monkey.velocityY + 0.9;
  
  if(gameState == play) {
    
    ground.velocityX = -4;
    
    monkey.visible = true;
      
    ground.x = ground.width/2;
    
    survivalTime=Math.round(frameCount/frameRate());

    
    if(keyDown("space") && monkey.y >= 340) {
      
      monkey.velocityY = -17;
      
    }
    
    if(monkey.isTouching(bananaGroup)) {
      
      bananaGroup.destroyEach();
      score = score+1;
      
    }
    
    if (monkey.isTouching(obstacleGroup)) {
      
      gameState = end;
      
    }
    
    Thebanana();
    Theobstacle();
    
  }
  
   if (gameState == end) {
     
     ground.velocityX = 0;
     
     monkey.visible = false;
     
    bananaGroup.setVelocityXEach(0);
    obstacleGroup.setVelocityXEach(0);
    
    bananaGroup.setLifetimeEach(-1);
    obstacleGroup.setLifetimeEach(-1);
    
  }
  
  drawSprites();
}

function Thebanana() {
  if(frameCount % 150 == 0) {
  banana = createSprite(590,Math.round(random(120,200)),10,10);
  banana.addImage("banana",bananaImage);
  banana.scale = 0.1;
  banana.velocityX = -5;
  banana.setlifetime = 150;
  bananaGroup.add(banana);
  }
}

function Theobstacle() {
  
  if(frameCount % 300 == 0) {
    obstacle = createSprite(590,363,10,10);
    obstacle.addImage("obstacle'sImg",obstacleImage);
    obstacle.scale = 0.15;
    obstacle.velocityX = -6.5;
    obstacle.lifetime = 120;
    obstacleGroup.add(obstacle);
    
  }
  
}


