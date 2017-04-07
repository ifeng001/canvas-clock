<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<style type="text/css">
		*{padding:0;margin:0;}
		#canvas{box-shadow: 2px 2px 5px black;margin:50px;background: skyblue;}
	</style>
</head>
<body>
	<canvas id="canvas" width="500" height="500"></canvas>
</body>
	<script type="text/javascript">
		var canvas = document.querySelector("#canvas");
		var ctx = canvas.getContext("2d");

		function drowClock(){
			//清除画布
				ctx.clearRect(0, 0, 800, 800);
				var now = new Date();
				var secd = now.getSeconds();
				var min = now.getMinutes();
				var hour = now.getHours();
				hour = hour + (min / 60);
				hour = hour > 12 ? hour - 12 : hour;
			//背景
				ctx.beginPath(); 
				ctx.lineWidth = 5; 
				ctx.strokeStyle = "blue"; 
				ctx.arc(250,250,200,0,360,false); 
				ctx.stroke(); 
				ctx.closePath(); 
				for(var i=0;i<12;i++){
						ctx.save();
						ctx.lineWidth=7;
						ctx.strokeStyle = "black";
						ctx.translate(250,250);
						ctx.rotate(Math.PI*i/6);
						ctx.beginPath();
						ctx.moveTo(0,-170);
						ctx.lineTo(0,-190);
						ctx.stroke(); 
						ctx.closePath();
						ctx.restore();
				}
				for(var i=0;i<60;i++){
					ctx.save();
					ctx.lineWidth=5;
					ctx.strokeStyle ="black";
					ctx.translate(250,250);
					ctx.rotate((Math.PI/30)*i);
					ctx.beginPath();
					ctx.moveTo(0,-180);
					ctx.lineTo(0,-190);
					ctx.stroke();
					ctx.closePath();
					ctx.restore();
				}
			// 动画
				//时针
				ctx.save();
				ctx.lineWidth = 7;
				ctx.strokeStyle = "#333";
				ctx.translate(250, 250);
				ctx.rotate(hour * 30 * Math.PI / 180);
				ctx.beginPath();
				ctx.moveTo(0, -120);
				ctx.lineTo(0, 20);
				ctx.lineCap="round";
				ctx.stroke();
				ctx.closePath();
				ctx.restore();

				//分针
				ctx.save();
				ctx.lineWidth = 5;
				ctx.strokeStyle = "#333";
				ctx.translate(250, 250);
				ctx.rotate(min * 6 * Math.PI / 180);
				ctx.beginPath();
				ctx.moveTo(0, -140);
				ctx.lineTo(0, 20);
				ctx.lineCap = "round";
				ctx.stroke();
				ctx.closePath();
				ctx.restore();

				//秒针
				ctx.save();
				ctx.lineWidth = 3;
				ctx.strokeStyle = "#f00";
				ctx.translate(250, 250);
				ctx.rotate(secd * 6 * Math.PI / 180);
				ctx.beginPath();
				ctx.moveTo(0,-178);
				ctx.lineTo(0,30);
				ctx.lineJoin="round";
				ctx.closePath();
				ctx.stroke();

			// 秒针及交叉点装饰
				// 秒针装饰
		 		ctx.beginPath();     
		 		ctx.arc(0,-155,5,0,360,false);     
		 		ctx.closePath();
		 		ctx.strokeStyle="red"; 
		 		ctx.fillStyle = "white";
		 		ctx.fill(); 
		 		ctx.stroke();  
		 		ctx.restore();
		 		// 交叉点装饰
		 		ctx.beginPath();
				ctx.arc(250, 250, 5, 0, 360, false);
				ctx.closePath();
				ctx.lineWidth=3;
				ctx.strokeStyle = "red";
				ctx.fillStyle = "white";
				ctx.fill();
				ctx.stroke();
				ctx.restore();
		}

		drowClock();
		setInterval(function(){
			drowClock();
		}, 1000);
	</script>
</html>
