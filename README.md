<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title>Jquery Ajax</title>
		<!-- Latest compiled and minified CSS -->
		<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">

		<!-- Optional theme -->
		<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap-theme.min.css" integrity="sha384-rHyoN1iRsVXV4nD0JutlnGaslCJuC7uwjduW9SVrLvRYooPp2bWYgmgJQIXwl/Sp" crossorigin="anonymous">
		
		<script   src="https://code.jquery.com/jquery-3.1.1.min.js"   integrity="sha256-hVVnYaiADRTO2PzUGmuLJr8BLUSjGIZsDYGmIJLv2b8="   crossorigin="anonymous"></script>
		<!-- Latest compiled and minified JavaScript -->
		<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
		<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/lazysizes/2.0.4/lazysizes-umd.min.js"></script>
	</head>

	<body>
		<section class="container">
			<nav class="navbar navbar-default">
				<div class="container-fluid">
					<!-- Brand and toggle get grouped for better mobile display -->
					<div class="navbar-header">
						<button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
							<span class="sr-only">Toggle navigation</span>
							<span class="icon-bar"></span>
							<span class="icon-bar"></span>
							<span class="icon-bar"></span>
						</button>
						<a class="navbar-brand" href="#">Brand</a>
					</div>

					<!-- Collect the nav links, forms, and other content for toggling -->
					<div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
						<ul class="nav navbar-nav">
							<li class="dropdown">
							  <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">All <span class="caret"></span></a>
							  <ul class="dropdown-menu"></ul>
							</li>
						</ul>
					</div><!-- /.navbar-collapse -->
				</div><!-- /.container-fluid -->
			</nav>
		</section>
		<style>
			figure{margin-bottom:10px;}
		</style>
		<section id="jsonContainer" class="container clearfix">
		
			<script>
				$(document).ready(function(){
					var root = 'https://jsonplaceholder.typicode.com';
					$.ajax({
					  url: root + '/photos/',
					  method: 'GET'
					}).then(function(data) {
						var albums = data;
						var template = '';
						var navLinks ='';
						navLinks+='<li class="album-1">';
							navLinks+='<a href="1">Album 1</a>';
						navLinks+='</li>';
						var albumId = 1;
						$.each(albums, function(){
							if(albumId!=this.albumId)
							{
								albumId = this.albumId;
								navLinks+='<li class="album-'+this.albumId+'">';
									navLinks+='<a href="'+this.albumId+'">Album '+this.albumId+'</a>';
								navLinks+='</li>';
							}
							
							template+='<figure class="col-md-2 col-xs-6 album-'+this.albumId+'">';
								template+='<img src="'+this.thumbnailUrl+'" class="img-responsive lazyload"/>';
								template+='<figcaption>'+this.title+'</figcaption>';
							template+='</figure>';
						});
						$('.dropdown-menu').html(navLinks);
						$('#jsonContainer').html(template);
						$('.dropdown-menu li a').click(function(e){
							e.preventDefault();
							$('.dropdown-toggle').html($(this).text()+'<span class="caret"></span>');
							toShow = $('figure.album-'+$(this).attr('href'));
							album = $(this).attr('href');
							$.each($('figure'), function(){
								if($(this).hasClass('album-'+album))
								{
									$(this).show();
								}
								else
								{
									$(this).hide();
								}
							});
						});
					});
				});
			</script>
		</section>
	</body>

</html>
