# 页面结构

>html

    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=0" />
      <meta name="renderer" content="webkit">
      <title>患者管理</title>
      <meta name="keywords" content="">
      <meta name="description" content="">
      <link href="css/bootstrap.min.css" rel="stylesheet">
      <link href="css/plugins/fontAwesome/css/font-awesome.min.css" rel="stylesheet" media="all" />
      <link href="css/plugins/jQueryUI/jquery-ui-1.10.4.custom.min.css" rel="stylesheet">
      <!-- Data Tables -->
      <link href="css/plugins/jqgrid/ui.jqgrid.css" rel="stylesheet">
      <link href="css/plugins/zTree/zTreeStyle/zTreeStyle.css" rel="stylesheet">
      <!-- sobox -->
      <link href="css/plugins/sobox/sobox.css" rel="stylesheet">
      <!-- viewer.css -->
      <link href="css/plugins/viewer/viewer.css" rel="stylesheet">
      <link href="css/animate.css" rel="stylesheet">
      <link href="css/style.css" rel="stylesheet">
      <style media="screen">
        table th{font-weight: 800;}
      </style>
    </head>
    <body>
      <div id="wrapper">
        <nav class="navbar-default navbar-static-side" role="navigation">  //导航
          .....
        </nav>
        <div id="page-wrapper" class="gray-bg dashbard-1">
          <div class="row border-bottom">
              <nav class="navbar navbar-static-top" role="navigation" style="margin-bottom: 0">
                ...          //头部图标和退出
              </nav>
          </div>
          <div class="row wrapper border-bottom white-bg page-heading">
              <div class="col-lg-10" style="padding-top:20px;">
                ...          //页面导航栏
              </div>
          </div>
          <div class="wrapper wrapper-content animated fadeInRight">
            <div class="jqGrid_wrapper animated fadeInRight jqGrid_resize" id="info_grid">
              <div class="" style="display:inline-block;padding-bottom:25px;">
                <div class="searchBox" id="searchBox">
                  <select class="" name="jqGridSearchField" id="jqGridSearchField" autocomplete="off">

                  </select>
                  <input type="text" name="jqGridSearchString" value="" placeholder="" autocomplete="off" id="jqGridSearchString">
                  <select class="" name="jqGridSearchState" id="jqGridSearchState" autocomplete="off" style="margin-left:10px;" hidden="hidden">
                  </select>
                  <button type="button" name="searchBtn" id="jqGridSearchQuery">查询</button>
                  <button type="button" name="searchBtn" id="jqGridSearchReset">重置</button>
                </div>
              </div>
              <table id="table_query"></table>
              <div id="pager_query"></div>  ／／搜索框
            </div>
            <div class="actpage_wrapper">
              <div class="actpage animated fadeInRight" id="info_get" style="display:none">
                ...          //get页面 (得到)
              </div>
              <div class="actpage animated fadeInRight" id="info_add" style="display:none">
                ...          //add页面 (新增)
              </div>
              <div class="actpage animated fadeInRight" id="info_update" style="display:none">
                ...          //update页面 (编辑)
              </div>
            </div>
          </div>
        </div>
      </div>
    </body>
    </html>
