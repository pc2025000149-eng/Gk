# Gk<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>정치 참여 어드벤처</title>
  <script src="https://cdn.jsdelivr.net/npm/phaser@3.55.2/dist/phaser.min.js"></script>
  <style>
    body { margin: 0; padding: 0; background: #111; color: white; font-family: sans-serif; }
    #game-container { width: 100%; height: 100vh; display: flex; align-items: center; justify-content: center; }
  </style>
</head>
<body>
  <div id="game-container"></div>
  <script>
    class MainScene extends Phaser.Scene {
      constructor() {
        super('MainScene');
      }

      preload() {
        // 간단한 사각형 Base64 스프라이트 (플레이어/시민)
        this.load.image('player', 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAMAAAAoLQ9TAAAAQlBMVEUAAAD///////////////////////////////////////////////////////////////////////////////////////////////////9PQkWqAAAADXRSTlMAESIzRGZ2f4aXycvQ1wa9lQAAAHhJREFUGNNVzcsSgCAMBNDHOBUQB37/Z7EtpCkQKC4U5jHpwFGxMw0pOSo12H1hYgscK6l+VsuGF3cBe+Fbhf53cFVNQ4llGQUwQzVR7W0O6hd+fS7QvVviuP5Z1COyB9KCbDR1Mg2QwQwdO7FUzqBpSQAAAAASUVORK5CYII=');
        this.load.image('npc', 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAMAAAAoLQ9TAAAAUVBMVEUAAAD///////////////////////////////////////////////////////////////////////////////////////////////////////9jhPqzAAAAG3RSTlMAESIzRGZ2eYmVn6C5v8zX19vg6Orv8vP5+gITJZoAAAB1SURBVBjTjY5LDsAgCEXdMg9wPv//U0pQhsKW2P7XGdEFS5ywlGq9IjKkI7cQSRdjUkVd8rXwsMktS1pKNxA4WYnETrpA2auimD1rB6bAQ3uDXYrO7iz8dKZ64+fMawKcGZaz43zvwxJdQ0xOJjEPW7QYsdPQH8AAAAASUVORK5CYII=');
      }

      create() {
        this.add.text(20, 20, "정치 참여 어드벤처 🎮", { fontSize: '18px', fill: '#fff' });

        this.player = this.physics.add.sprite(100, 100, 'player').setScale(2);
        this.npc = this.physics.add.sprite(250, 150, 'npc').setScale(2);

        this.cursors = this.input.keyboard.createCursorKeys();

        this.dialog = this.add.text(20, 250, "NPC에게 다가가서 대화하세요.", { fontSize: '14px', fill: '#0f0' });

        this.physics.add.overlap(this.player, this.npc, this.talk, null, this);
      }

      update() {
        this.player.setVelocity(0);
        if (this.cursors.left.isDown) this.player.setVelocityX(-150);
        else if (this.cursors.right.isDown) this.player.setVelocityX(150);
        if (this.cursors.up.isDown) this.player.setVelocityY(-150);
        else if (this.cursors.down.isDown) this.player.setVelocityY(150);
      }

      talk() {
        this.dialog.setText("시민: 우리 함께 정치에 참여해요!\n👉 투표, 시위, 서명 운동, 청원 등 다양한 방법이 있어요.");
      }
    }

    const config = {
      type: Phaser.AUTO,
      width: 400,
      height: 300,
      parent: "game-container",
      physics: { default: 'arcade', arcade: { debug: false } },
      scene: [MainScene]
    };

    new Phaser.Game(config);
  </script>
</body>
</html>

gk
