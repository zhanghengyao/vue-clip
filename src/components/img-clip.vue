<template>
	<div>
		<div id="clip_container">
			<canvas></canvas>
			<footer>
				<div data-box="_box1_">
					<img :src="cancelSrc" alt="">
				</div>
				<div data-box="_box2_">
					<img :src="leftRotateSrc" alt="">
				</div>
				<div data-box="_box3_">
					<img :src="rightRotateSrc" alt="">
				</div>
				<div data-box="_box4_">
					<img :src="okSrc" alt="">
				</div>
			</footer>
		</div> 		
	</div>
</template>
<style scoped>
	footer{
		position : 'fixed';
		bottom : 0;
		left : 0;
		width : '100%';
		height : '50px';
		background-color : '#000';
	    text-align : 'center';
		line-height : '70px';
	}
	footer div{
		float : 'left';
		width : '25%';
	}
</style>
<script>
	export default{
		props: {
			cutRectSize: {
				type: Number,
				required: false,
				default: 200
			},
			img:{
				type: [String, Image, HTMLImageElement, HTMLCanvasElement],
				required: true
			}
		},
		data() {
			return {
				cancelSrc = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAABTklEQVRYR+2W303EMAzGbSkzVGqyBBvcbQJsABNwNwGMcGxSNmCJ5qEzVAqKlKIqShp/LlJ5uL7WzvfznzhmOvjjg/XpDvA/MzBN08M8z+/MPPR9f93TJ+M4Xpj5ZIx57bruOz+rmAHv/UBEp2gcQrg55541EN77GxE9Jt8va+1ZBJCo3xZjDUQmHgO5OucuIoBoVDhAnIncl4g+rbVPpSxuNqEGAhGPQM1bgECg4iIAaTk04mKAFoRWHAKoQTBzLONy1aJZteHgJiw5FKJdm0HicAYWpQoELP6nAJphpQLYKoEGojkH1gUudXv6/9uEKIQYYOuqIcNK/Ba0Is9nuxaimQFkyGggoMdIMmRQiCoAEnleVwSiCJAvJJLIBRDyhWS9kmnEKxNTvpKlpfQjhDCU1ihkP0zZPBtjXsRLKSKw17Z5DfcKtPzvAIdn4AeHGf8hqLdyawAAAABJRU5ErkJggg==',
	 			okSrc = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAABP0lEQVRYR+2WsW3DMBBF7yCqjioVVJMRkhG8QTawM0GQDTyCN7CzQUbIBvEIaUQCapROjYALTogNGxEt6mjKRcRKBYH3RN59HsKNF96YD7PA/zsBa+19kiRZnud7rr9JT8AYswGAFwYT0a4oiufJBIwxOwBYnnYdIi4mEeiDs4hS6jG6gAsOAG9a61VUgSF41CL0gUcT8IUfBcqyXHN7IOJeKfV66FHJOzEG3glUVfXQtu3nAUZE32maLiQSY+GdgLV2RUTb07+VSEjgnUBd11nTNF8AcCeVkMKPNfB7DR8SiRD4WRdIJELhf9pwjMQ14L054CNxLbgziC5JICLXylNPRnTZPjY7nG+BS8IBEMEHo9hTQgwfFOANAxJBcC+BCxLBcG8B3sjDJBHxTJcBwLvWmr+DV9SBxMduFphP4AcU3t8E8fazCwAAAABJRU5ErkJggg==',				
	 			rightRotateSrc = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAC2UlEQVRYR9WXXW7TQBDH/2ObSkgQe1XnmXICwglIT9ByAtoTEE5AeoK2JyCcoOYEpCcg3KB9TqS1A1Il5HjQOrbjz3jjBlXkJQ+7s/Obj/3PmvDEP3pi//g/AKR8OIqMPyfMfJpkbJD8zwD4MAzPXD27FeL53a4Z3ZoBKX8PVhReAjTUOpgwMaODi11AGgEWMrgC4aOW49ImIowObftax7YCICU7KwpuKlEzBwB5DNwRSKXeYfARAQMQTirOCBPXts/bICoAc+nPiOhNZsgcEGh8KOyrpsMUdIjliMAjENnZPg2IAsBCBhMQPqQHMPNPC/ZQCPLbIlHrqmdChJN8AMy46At73GSfAczlryFR9D3vvC+ctNt1/Md71tkIpnkIkw9eNzVmDsBXRu/iU5jvTdgD3cjLdPHtQTjNysH46gr7rC6KGGB93VY/NnWnc1f0Jtph12ycy2BMhM/pksk9URdQDFDYzHzvCufoMc7TUqxoKduCSgDy6ce1K+zRYwGU/UIGXnZFGd9cYadKmrso8Ubf39SL3rui5+0DIJ9ZZr7tC6eiqHEGFn7Am+43jvvi5bQLgOolWJzpQBRFQ2YkV5B90zQ3GQgpEOLFbO8Ahe5vioI5MGEN9w6wrvvyDMRftmaQN2X+J024FYKLV3xdgtzkY/Cs7zhvu/RA3qasA2t9q8pykoGyDHdvxDxEYbY0qGEmxQvp34HoVUy6pyxkWgD4W6U4aZ5TEN/kFEJrnreVSg0ntadprhTG8VzmFFFZaczzNoC29QJA3ShV5QCbn9rESY1z0OrSYutc3e82x+l6zZMsHqVe2g+ZQoJnBtHEMIz48DAEWRZ4rXZ8BlAywNg32TrWhah9lCaZ8LL3gW44G9rG+V8+auuzPBYURONyNhp5mO8BY7TLMNP6MlrI5SmgPkp4WIGJnarXsuG19UkduBZA2VCVqOtzbacS7Fr6Lvs7ZaCLoyabv5v+ajCtwZRVAAAAAElFTkSuQmCC',
				leftRotateSrc = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAC30lEQVRYR+2WbU7bQBCG37EjoUol9qrO77onaHoC0hM0PQHhBA0nIJyg6QmAExBO0HCCpico/E6ktVMkRGVnql3H2HH8SZBQpVrKDzs7O8/OxztLeOGHXtg//k0AKe+6KyM8YOZ+FEHqAXwDQP08GMbEDPevhCCvKsKNIjCXv3tE4UnksPphwri1ap+WgdQCkJLtkPwzgNYnrnaerGAPbBw7on2eZ1UJIOW9G9DDJYG6Gxsw+wBNWIfdmBLYZbBLQBeET1lnKhodyzrOfi8FUCcPyP++4Zz5FjBGRSdSDnTEsByB8CXtkBmnHWGN0t9KAebSmxLRwaMB48JEe1inuCKQu26IYAoiK9mDPjuiPYnfCwEWcjkA8VnauSOsQZPsRxD3boiHWQLBnsnWu/gQJQDeDYjeqk2Y+WdH2Js10IBER4LCH7FJOhW5AAu57IP4MjEwPnbE/rSBz62lC+mfg3AY/cGeY9tCK0jepunFu54+3l+ngv78it9NNj8I8XpWAOB5cc6IcfxGWONdTh/bLmQ6rVFH5AN4Pj9n+BMAf/zYmowrR1h9DaAkttWCdhoyu1hxoloG9U1KaXrQuhXildL8xs9c+iMinKwL+7oj7J4G2Gq5gq1VPbRg9erqQHabQoAIIl2lOQTMvom97lNPv/aRn4JUjlKtkoLQzls9VbWN454ymEtvRkTvoxQUFOGW/OrFu+tAtg3BkSRvdYEeQPDVDNCkYDoqGzx1I5LOP5h9R9h2oRA9QsAYP4fzrBSDcRHPlcJZoEK2S8ElCpgZ6bqeLLdyGNUNbdm6vPtE9k5QeSNKO4j0YnVo8t5RVXTWa78CpHMd1VMS+vhTbYBtsWJVqBPDMGZBAIqVNFit+qRvy+RuRIdxZaI9yIpYLYCtzmiaH8Y3R1jDPLNaALGhbiXwcOOKVQLDzNeAOSq7SzQCSBRzOQBUmLmXhVHzgkBTE+Z5HeV8EkDTDJSt/w/wF0QXejAZ0e4bAAAAAElFTkSuQmCC',
		
			}
		}
	}
</script>