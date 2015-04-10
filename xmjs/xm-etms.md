---
layout: xm_page
title: 电力收费系统
---
####采用工具               
- Java,swt,windowsBuilder
- Hibernate,Mysql           

***         

####个人职责/动机              
帮人写软著，完成了从数据库设计到实现所有功能。            

***        

####主要功能                
包含了基本的登陆，用户管理，电力收费，抄表，查询等相关操作。          

***          

####部分功能示例          
- 登陆界面            
![login](/img/ETMS/login.png)      
- 主界面     
![login](/img/ETMS/main.png)      
- 用户管理界面       
![login](/img/ETMS/user.png)       
- 收费界面      
![login](/img/ETMS/charge.png)       
- 历史查询界面      
![login](/img/ETMS/jiaofei.png)       

***      
    
####部分代码      

**抄表计算**           
           
> 
    @Override
    public void widgetSelected(SelectionEvent e) {
    	MessageBox mb = new MessageBox(shell,SWT.ICON_QUESTION | SWT.OK| SWT.CANCEL);
    	try{
    		int row = table.getSelectionIndex();
    		if(bccbdl.getText().equals("")||row<0){
    			mb.setText("提示");
    			mb.setMessage("请选择一条数据，并填写本次抄表电量！");
    			mb.open();
    			return;
    		}
    		TableItem item =table.getItem(row);
    		String yhid=item.getText(0);//用户ID
    		//计算价格并扣除使用电量
    		BaseBll b=new BaseBll();
    		List l =b.load("select cbdl from GetData where yhid='"+yhid+"' and sfqy='是'");
    		double scdl=(Double) l.get(0);//上次电量
    		double dqdl=Double.parseDouble(bccbdl.getText());//当前电量
    		if(dqdl<=scdl){
    			mb.setText("提示");
    			mb.setMessage("请确保当前电量大于上次电量！！");
    			mb.open();
    			return;
    		}
    		double cha=dqdl-scdl;
    		List stand =b.load("select a.feestandard from PowerType a,UserInfo b where a.id=b.powertypeID and b.yhid='"+yhid+"'");
    		double standard=Double.parseDouble(stand.get(0).toString());
    		double ye=Double.parseDouble(yhye.getText())-cha*standard;
    		String hql = "update UserInfo set yhye='"+ye+"' where yhid='"+yhid+"'";
    		b.update(hql);
    		//之前的记录更新为否
    		if(!b.load("select gdid from GetData where yhid='"+yhid+"'").isEmpty()){
    			b.update("update GetData set sfqy='否' where yhid='"+yhid+"'");
    		}
    		//新建抄表记录
    		GetData g =new GetData();
    		g.setYhid(Integer.parseInt(yhid));
    		g.setCbrq(new Date());
    		g.setSfqy("是");
    		g.setCbdl(Double.parseDouble(bccbdl.getText()));
    		b.add(g);
    		mb.setText("提示");
    		mb.setMessage("保存成功!");
    		mb.open();
    		yhye.setText(String.valueOf(ye));
    		table.removeAll();
    		initTableItem();
    	}catch(Exception e1){
    		mb.setText("提示");
    		mb.setMessage("请确保信息填写正确，保证本次抄表电量为数字！");
    		mb.open();
    	}
    }
