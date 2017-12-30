package practicesss;

import java.awt.BorderLayout;
import java.awt.Component;
import java.awt.Container;
import java.awt.Dimension;
import java.awt.FileDialog;
import java.awt.FlowLayout;
import java.awt.Font;
import java.awt.GraphicsEnvironment;
import java.awt.GridLayout;
import java.awt.Toolkit;
import java.awt.datatransfer.Clipboard;
import java.awt.datatransfer.DataFlavor;
import java.awt.datatransfer.StringSelection;
import java.awt.datatransfer.Transferable;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.*;
import javax.swing.text.Document;
import javax.swing.JTextArea; 
import javax.swing.text.PlainDocument;  

import javax.swing.*;
import javax.swing.event.DocumentEvent;
import javax.swing.event.ListSelectionEvent;
import javax.swing.event.ListSelectionListener;
import javax.swing.event.UndoableEditEvent;
import javax.swing.event.UndoableEditListener;
import javax.swing.undo.CannotUndoException;
import javax.swing.undo.UndoManager;
import javax.swing.undo.*;
import practicesss.notepad.UndoHandler;



public class MainFrame extends JFrame{
	//设置组件
	
	private JMenuBar menuBar; 	//菜单条
	private JMenu fileMenu;		//文件菜单
	private JMenu editMenu;		//编辑菜单
	private JMenu formatMenu;	//格式菜单
	private JMenu viewMenu;		//查看菜单
	private JMenu helpMenu;		//帮助菜单
	
	private NotePadFrame f;
	
	private JTextArea jTextArea;	//文本区域
	private JScrollPane jScrollPane;		//滚动条
	//文件菜单内四项
	private JMenuItem openItem, closeItem, saveItem,aboutItem;	
	private JMenuItem newItem, savetoItem;		//新建项目，另存为项目
	//编辑菜单中的所有项目
	private JMenuItem editUndo, editCut, editCopy, editPaste, editDelete, editFind, editFindnext, editReplace, editGoto, editAll, editDates;
	//格式菜单下的项目
	private JMenuItem formatFont;		//字体
	private JCheckBoxMenuItem formatLinewrap;	//自动换行
	//查看菜单下的项目
	private JCheckBoxMenuItem Status;
	
	private FileDialog open,save;		//定义一个打开文件和保存文件
	private File file;  	//定义一个文件
	
	String fileName,copy,paste,cut;
	
//	public UndoManager undoMgr = new UndoManager();
	
	
	
	class UndoHandler implements UndoableEditListener
	{ public void undoableEditHappened(UndoableEditEvent uee)
	{ undo.addEdit(uee.getEdit());
	}
	}
	public void removeUpdate(DocumentEvent e)
	{ editUndo.setEnabled(true);
	}
	public void insertUpdate(DocumentEvent e)
	{ editUndo.setEnabled(true);
	}
	public void changedUpdate(DocumentEvent e)
	{ editUndo.setEnabled(true);
	}//DocumentListener结束
	
	//系统剪切板调用
	Toolkit toolkit=Toolkit.getDefaultToolkit();
	Clipboard clipBoard=toolkit.getSystemClipboard();
	//创建撤销操作管理器(与撤销操作有关)
	protected UndoManager undo=new UndoManager();
	protected UndoableEditListener undoHandler=new UndoHandler();
	
	protected Component statusLabel;
//	jTextArea.addUndoableEditListener(undo); 
	
	
	MainFrame() {		
		Init();
	}
	
	//初始化
	public void Init(){		
		JFrame frame = new JFrame("Wangha's Text");		//建立一个名为记事本·伪的窗口
		frame.setBounds(300, 300, 700, 450);		//窗口位置在300，300，窗口大小为700*450
		frame.setDefaultCloseOperation(EXIT_ON_CLOSE);		//
		
		menuBar = new JMenuBar();		//初始化菜单栏
		fileMenu = new JMenu("文件");		//初始化名为文件的文件菜单
		editMenu = new JMenu("编辑");		//初始化编辑菜单
		formatMenu = new JMenu("格式");	//初始化格式菜单
		viewMenu = new JMenu("查看");		//初始化查看菜菜的那
		helpMenu = new JMenu("帮助");		//初始话名为帮助的帮助菜单
		
//		Document doc = jTextArea.getDocument();
		
		jTextArea = new JTextArea(10, 40);		//10行40列
		Font x = new Font("Monospaced",1,20);	//定义字体大小以及一些属性
		
		jTextArea.setFont(x);		//只能使用x这种字体
		jTextArea.setLineWrap(true);//到达指定宽度则换行
		//应当首先利用构造函数指定JScrollPane的控制对象，此处为JTextArea，然后再讲JScrollPane
		
		jScrollPane = new JScrollPane(jTextArea);	//将滚动条添加进面板
		//设置滚动条自动出现
		jScrollPane.setHorizontalScrollBarPolicy( JScrollPane.HORIZONTAL_SCROLLBAR_AS_NEEDED); //水平
		jScrollPane.setVerticalScrollBarPolicy(JScrollPane.VERTICAL_SCROLLBAR_AS_NEEDED); //竖直
		jScrollPane.setViewportView(jTextArea);
		
		jTextArea.getDocument().addUndoableEditListener(undo);	
		
		//定义文件菜单内部的功能菜单
		newItem = new JMenuItem("新建");
		openItem = new JMenuItem("打开");
		saveItem = new JMenuItem("保存");
		savetoItem = new JMenuItem("另存为");
		closeItem = new JMenuItem("关闭");
		//定义编辑菜单内部项目
		editUndo = new JMenuItem("撤销");
		editCut = new JMenuItem("剪切");
		editCopy = new JMenuItem("复制");
		editPaste = new JMenuItem("粘贴");
		editDelete = new JMenuItem("删除");
		editFind = new JMenuItem("查找");
		editReplace = new JMenuItem("替换");
		editGoto = new JMenuItem("转到");
		editAll = new JMenuItem("全选");
		editDates = new JMenuItem("时间");
		//格式菜单
		formatFont = new JMenuItem("字体");
		formatLinewrap = new JCheckBoxMenuItem("自动换行");
		//查看菜单
		Status = new JCheckBoxMenuItem("状态栏");
		//帮助菜单
		aboutItem = new JMenuItem("关于");
		
		//添加两个选项卡到JMenu
		//添加子菜单项到菜单项
		menuBar.add(fileMenu);
		menuBar.add(editMenu);
		menuBar.add(formatMenu);
		menuBar.add(viewMenu);
		menuBar.add(helpMenu);
		
		fileMenu.add(newItem);
		fileMenu.add(openItem);
		fileMenu.add(saveItem);
		fileMenu.add(savetoItem);
		fileMenu.add(closeItem);	
		editMenu.add(editUndo);
		editMenu.add(editCut);
		editMenu.add(editCopy);
		editMenu.add(editPaste);
		editMenu.add(editDelete);
		editMenu.add(editFind);
		editMenu.add(editReplace);
		editMenu.add(editGoto);
		editMenu.add(editAll);
		editMenu.add(editDates);
		formatMenu.add(formatLinewrap);
		formatMenu.add(formatFont);
		viewMenu.add(Status);
		helpMenu.add(aboutItem);
		//放置菜单项及输入框
		
		frame.add(menuBar, BorderLayout.NORTH);
		frame.add(jScrollPane, BorderLayout.CENTER);
		
		statusLabel=new JLabel("　按F1获取帮助");
		frame.add(statusLabel,BorderLayout.SOUTH);//向窗口添加状态栏标签
		statusLabel.setVisible(false);

		//FileDialog 类显示一个对话框窗口，用户可以从中选择文件。 
		//由于它是一个模式对话框，当应用程序调用其 show 方法来显示对话框时，它将阻塞其余应用程序，直到用户选择一个文件。 
		open = new FileDialog(frame,"打开文档",FileDialog.LOAD);	//打开文档时候的界面
	    save = new FileDialog(frame,"保存文档",FileDialog.SAVE); 	//保存文档时候的界面
		
	    Event();												//四个按钮的监听
	    frame.setVisible(true);									//显示界面
	    
	}
	public JTextArea getTa() {
		  return jTextArea;
		 }
	public void checkMenuItemEnabled()
	{ String selectText=jTextArea.getSelectedText();
	if(selectText==null)
	{ editCut.setEnabled(true);
//	popupCut.setEnabled(false);
	editCopy.setEnabled(true);
//	popupCopy.setEnabled(false);
	editDelete.setEnabled(true);
//	popupMenu_Delete.setEnabled(false);
	}
	else
	{ editCut.setEnabled(true);
//	popupMenu_Cut.setEnabled(true); 
	editCopy.setEnabled(true);
//	popupMenu_Copy.setEnabled(true);
	editDelete.setEnabled(true);
//	popupMenu_Delete.setEnabled(true);
	}
	}
	
	//查找方法
	public void find()
		{ final JDialog findDialog=new JDialog(this,"查找",false);//false时允许其他窗口同时处于激活状态(即无模式)
		Container con=findDialog.getContentPane();//返回此对话框的contentPane对象 
		con.setLayout(new FlowLayout(FlowLayout.LEFT));
		JLabel findContentLabel=new JLabel("查找内容(N)：");
		final JTextField findText=new JTextField(15);
		JButton findNextButton=new JButton("查找下一个(F)：");
		final JCheckBox matchCheckBox=new JCheckBox("区分大小写(C)");
		ButtonGroup bGroup=new ButtonGroup();
		final JRadioButton upButton=new JRadioButton("向上(U)");
		final JRadioButton downButton=new JRadioButton("向下(U)");
		downButton.setSelected(true);
		bGroup.add(upButton);
		bGroup.add(downButton);
		/*ButtonGroup此类用于为一组按钮创建一个多斥（multiple-exclusion）作用域。
		使用相同的 ButtonGroup 对象创建一组按钮意味着“开启”其中一个按钮时，将关闭组中的其他所有按钮。*/
		/*JRadioButton此类实现一个单选按钮，此按钮项可被选择或取消选择，并可为用户显示其状态。
		与 ButtonGroup 对象配合使用可创建一组按钮，一次只能选择其中的一个按钮。
		（创建一个 ButtonGroup 对象并用其 add 方法将对象包含在此组中。）*/
		JButton cancel=new JButton("取消");
		//取消按钮事件处理
		cancel.addActionListener(new ActionListener()
		{ public void actionPerformed(ActionEvent e)
		{ findDialog.dispose();		//将查找窗口释放内存，也就是关闭
		}
		});
		//"查找下一个"按钮监听
		findNextButton.addActionListener(new ActionListener()
		{ public void actionPerformed(ActionEvent e)
		{ //"区分大小写(C)"的JCheckBox是否被选中
		int k=0,m=0;
		final String str1,str2,str3,str4,strA,strB;
		str1=jTextArea.getText();
		str2=findText.getText();
		str3=str1.toUpperCase();
		str4=str2.toUpperCase();
		if(matchCheckBox.isSelected())//区分大小写
		{ strA=str1;
		 strB=str2;
		}
		else//不区分大小写,此时把所选内容全部化成大写(或小写)，以便于查找 
		{ strA=str3;
		 strB=str4;
		}
		if(upButton.isSelected())
		{ //k=strA.lastIndexOf(strB,editArea.getCaretPosition()-1);
		 if(jTextArea.getSelectedText()==null)
		 k=strA.lastIndexOf(strB,jTextArea.getCaretPosition()-1);//在strA中查找strB，往后查找
		 else
		 k=strA.lastIndexOf(strB, jTextArea.getCaretPosition()-findText.getText().length()-1); //往前查找
		 if(k>-1)
		 { //String strData=strA.subString(k,strB.getText().length()+1);
		 jTextArea.setCaretPosition(k);		//选中字符串
		 jTextArea.select(k,k+strB.length());
		 }
		 else
		 { JOptionPane.showMessageDialog(null,"找不到您查找的内容！","查找",JOptionPane.INFORMATION_MESSAGE);
		 }
		}
		else if(downButton.isSelected())
		{ if(jTextArea.getSelectedText()==null)
		 k=strA.indexOf(strB,jTextArea.getCaretPosition()+1);//index 返回第一个索引的位置，从这个位置开始搜索
		 else
		 k=strA.indexOf(strB, jTextArea.getCaretPosition()-findText.getText().length()+1); 
		 if(k>-1)
		 { //String strData=strA.subString(k,strB.getText().length()+1);
		 jTextArea.setCaretPosition(k);
		 jTextArea.select(k,k+strB.length());
		 }
		 else
		 { JOptionPane.showMessageDialog(null,"找不到您查找的内容！","查找",JOptionPane.INFORMATION_MESSAGE);
		 }
		}
		}
		});//"查找下一个"按钮监听结束
		//创建"查找"对话框的界面
		JPanel panel1=new JPanel();
		JPanel panel2=new JPanel();
		JPanel panel3=new JPanel();
		JPanel directionPanel=new JPanel();
		directionPanel.setBorder(BorderFactory.createTitledBorder("方向"));
		//设置directionPanel组件的边框;
		//BorderFactory.createTitledBorder(String title)创建一个新标题边框，使用默认边框（浮雕化）、默认文本位置（位于顶线上）、默认调整 (leading) 以及由当前外观确定的默认字体和文本颜色，并指定了标题文本。
		directionPanel.add(upButton);
		directionPanel.add(downButton);
		panel1.setLayout(new GridLayout(2,1));
		panel1.add(findNextButton);
		panel1.add(cancel);
		panel2.add(findContentLabel);
		panel2.add(findText);
		panel2.add(panel1);
		panel3.add(matchCheckBox);
		panel3.add(directionPanel);
		con.add(panel2);
		con.add(panel3);
		findDialog.setSize(410,180);
		findDialog.setResizable(false);//不可调整大小
		findDialog.setLocation(230,280);
		findDialog.setVisible(true);
	}//查找方法结束
	
	   
	//"字体"方法
	public void font()
	{ final JDialog fontDialog=new JDialog(this,"字体设置",false);
	Container con=fontDialog.getContentPane();
	con.setLayout(new FlowLayout(FlowLayout.LEFT));
	JLabel fontLabel=new JLabel("字体(F)：");
	fontLabel.setPreferredSize(new Dimension(100,20));//构造一个Dimension，并将其初始化为指定宽度和高度
	JLabel styleLabel=new JLabel("字形(Y)：");
	styleLabel.setPreferredSize(new Dimension(100,20));
	JLabel sizeLabel=new JLabel("大小(S)：");
	sizeLabel.setPreferredSize(new Dimension(100,20));
	final JLabel sample=new JLabel("Wangha's windowsText");
	final JTextField fontText=new JTextField(9);		//9列
	fontText.setPreferredSize(new Dimension(200,20));
	final JTextField styleText=new JTextField(8);
	styleText.setPreferredSize(new Dimension(200,20));
	final int style[]={Font.PLAIN,Font.BOLD,Font.ITALIC,Font.BOLD+Font.ITALIC};
	final JTextField sizeText=new JTextField(5);
	sizeText.setPreferredSize(new Dimension(200,20));
	JButton okButton=new JButton("确定");
	JButton cancel=new JButton("取消");
	cancel.addActionListener(new ActionListener()
	{ public void actionPerformed(ActionEvent e)
	{ fontDialog.dispose(); 
	}
	});
	Font currentFont=jTextArea.getFont();
	fontText.setText(currentFont.getFontName());
	fontText.selectAll();
	//styleText.setText(currentFont.getStyle());
	//styleText.selectAll();
	if(currentFont.getStyle()==Font.PLAIN)
	styleText.setText("常规");
	else if(currentFont.getStyle()==Font.BOLD)
	styleText.setText("粗体");
	else if(currentFont.getStyle()==Font.ITALIC)
	styleText.setText("斜体");
	else if(currentFont.getStyle()==(Font.BOLD+Font.ITALIC))
	styleText.setText("粗斜体");
	styleText.selectAll();
	String str=String.valueOf(currentFont.getSize());
	sizeText.setText(str);
	sizeText.selectAll();
	final JList fontList,styleList,sizeList;
	GraphicsEnvironment ge=GraphicsEnvironment.getLocalGraphicsEnvironment();
	final String fontName[]=ge.getAvailableFontFamilyNames();
	fontList=new JList(fontName);
	fontList.setFixedCellWidth(86);
	fontList.setFixedCellHeight(20);
	fontList.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
	final String fontStyle[]={"常规","粗体","斜体","粗斜体"};
	styleList=new JList(fontStyle);
	styleList.setFixedCellWidth(86);
	styleList.setFixedCellHeight(20);
	styleList.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
	if(currentFont.getStyle()==Font.PLAIN)
	styleList.setSelectedIndex(0);
	else if(currentFont.getStyle()==Font.BOLD)
	styleList.setSelectedIndex(1);
	else if(currentFont.getStyle()==Font.ITALIC)
	styleList.setSelectedIndex(2);
	else if(currentFont.getStyle()==(Font.BOLD+Font.ITALIC))
	styleList.setSelectedIndex(3);
	final String fontSize[]={"8","9","10","11","12","14","16","18","20","22","24","26","28","36","48","72"};
	sizeList=new JList(fontSize);
	sizeList.setFixedCellWidth(43);
	sizeList.setFixedCellHeight(20);
	sizeList.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
	fontList.addListSelectionListener(new ListSelectionListener()
	{ public void valueChanged(ListSelectionEvent event)
	{ fontText.setText(fontName[fontList.getSelectedIndex()]);
	fontText.selectAll();
	Font sampleFont1=new Font(fontText.getText(),style[styleList.getSelectedIndex()],Integer.parseInt(sizeText.getText()));
	sample.setFont(sampleFont1);
	}
	});
	styleList.addListSelectionListener(new ListSelectionListener()
	{ public void valueChanged(ListSelectionEvent event)
	{ int s=style[styleList.getSelectedIndex()];
	styleText.setText(fontStyle[s]);
	styleText.selectAll();
	Font sampleFont2=new Font(fontText.getText(),style[styleList.getSelectedIndex()],Integer.parseInt(sizeText.getText()));
	sample.setFont(sampleFont2);
	}
	});
	sizeList.addListSelectionListener(new ListSelectionListener()
	{ public void valueChanged(ListSelectionEvent event)
	{ sizeText.setText(fontSize[sizeList.getSelectedIndex()]);
	//sizeText.requestFocus();
	sizeText.selectAll(); 
	Font sampleFont3=new Font(fontText.getText(),style[styleList.getSelectedIndex()],Integer.parseInt(sizeText.getText()));
	sample.setFont(sampleFont3);
	}
	});
	okButton.addActionListener(new ActionListener()
	{ public void actionPerformed(ActionEvent e)
	{ Font okFont=new Font(fontText.getText(),style[styleList.getSelectedIndex()],Integer.parseInt(sizeText.getText()));
	jTextArea.setFont(okFont);
	fontDialog.dispose();
	}
	});
	JPanel samplePanel=new JPanel();
	samplePanel.setBorder(BorderFactory.createTitledBorder("示例"));
	samplePanel.add(sample);
	JPanel panel1=new JPanel();
	JPanel panel2=new JPanel();
	JPanel panel3=new JPanel();
	panel2.add(fontText);
	panel2.add(styleText);
	panel2.add(sizeText);
	panel2.add(okButton);
	panel3.add(new JScrollPane(fontList));//JList不支持直接滚动，所以要让JList作为JScrollPane的视口视图
	panel3.add(new JScrollPane(styleList));
	panel3.add(new JScrollPane(sizeList));
	panel3.add(cancel);
	con.add(panel1);
	con.add(panel2);
	con.add(panel3);
	con.add(samplePanel);
	fontDialog.setSize(350,340);
	fontDialog.setLocation(200,200);
	fontDialog.setResizable(false);
	fontDialog.setVisible(true);
	}
	
	
	//替换方法
	public void replace()
		{ final JDialog replaceDialog=new JDialog(this,"替换",false);//false时允许其他窗口同时处于激活状态(即无模式)
		Container con=replaceDialog.getContentPane();//返回此对话框的contentPane对象
		con.setLayout(new FlowLayout(FlowLayout.CENTER));
		JLabel findContentLabel=new JLabel("查找内容(N)：");
		final JTextField findText=new JTextField(15);
		JButton findNextButton=new JButton("查找下一个(F):");
		JLabel replaceLabel=new JLabel("替换为(P)：");
		final JTextField replaceText=new JTextField(15);
		JButton replaceButton=new JButton("替换(R)");
		JButton replaceAllButton=new JButton("全部替换(A)");
		JButton cancel=new JButton("取消");
		cancel.addActionListener(new ActionListener()
		{ public void actionPerformed(ActionEvent e)
		{ replaceDialog.dispose();
		}
		});
		final JCheckBox matchCheckBox=new JCheckBox("区分大小写(C)");
		ButtonGroup bGroup=new ButtonGroup();
		final JRadioButton upButton=new JRadioButton("向上(U)");
		final JRadioButton downButton=new JRadioButton("向下(U)");
		downButton.setSelected(true);
		bGroup.add(upButton);
		bGroup.add(downButton);
		/*ButtonGroup此类用于为一组按钮创建一个多斥（multiple-exclusion）作用域。
		使用相同的 ButtonGroup 对象创建一组按钮意味着“开启”其中一个按钮时，将关闭组中的其他所有按钮。*/
		/*JRadioButton此类实现一个单选按钮，此按钮项可被选择或取消选择，并可为用户显示其状态。
		与 ButtonGroup 对象配合使用可创建一组按钮，一次只能选择其中的一个按钮。
		（创建一个 ButtonGroup 对象并用其 add 方法将 JRadioButton 对象包含在此组中。）*/
		 
		//"查找下一个"按钮监听
		findNextButton.addActionListener(new ActionListener()
		{ public void actionPerformed(ActionEvent e)
		{ //"区分大小写(C)"的JCheckBox是否被选中
		int k=0,m=0;
		final String str1,str2,str3,str4,strA,strB;
		str1=jTextArea.getText();
		str2=findText.getText();
		str3=str1.toUpperCase();
		str4=str2.toUpperCase();
		if(matchCheckBox.isSelected())//区分大小写
		{ strA=str1;
		 strB=str2;
		}
		else//不区分大小写,此时把所选内容全部化成大写(或小写)，以便于查找 
		{ strA=str3;
		 strB=str4;
		}
		if(upButton.isSelected())
		{ //k=strA.lastIndexOf(strB,editArea.getCaretPosition()-1);
		 if(jTextArea.getSelectedText()==null)
		 k=strA.lastIndexOf(strB,jTextArea.getCaretPosition()-1);
		 else
		 k=strA.lastIndexOf(strB, jTextArea.getCaretPosition()-findText.getText().length()-1); 
		 if(k>-1)
		 { //String strData=strA.subString(k,strB.getText().length()+1);
			 jTextArea.setCaretPosition(k);
		 jTextArea.select(k,k+strB.length());
		 }
		 else
		 { JOptionPane.showMessageDialog(null,"找不到您查找的内容！","查找",JOptionPane.INFORMATION_MESSAGE);
		 }
		}
		else if(downButton.isSelected())
		{ if(jTextArea.getSelectedText()==null)
		 k=strA.indexOf(strB,jTextArea.getCaretPosition()+1);
		 else
		 k=strA.indexOf(strB, jTextArea.getCaretPosition()-findText.getText().length()+1); 
		 if(k>-1)
		 { //String strData=strA.subString(k,strB.getText().length()+1);
			 jTextArea.setCaretPosition(k);
			 jTextArea.select(k,k+strB.length());
		 }
		 else
		 { JOptionPane.showMessageDialog(null,"找不到您查找的内容！","查找",JOptionPane.INFORMATION_MESSAGE);
		 }
		}
		}
		});//"查找下一个"按钮监听结束
		 
		//"替换"按钮监听
		replaceButton.addActionListener(new ActionListener()
		{ public void actionPerformed(ActionEvent e)
		{ if(replaceText.getText().length()==0 && jTextArea.getSelectedText()!=null) 
			jTextArea.replaceSelection(""); 
		if(replaceText.getText().length()>0 && jTextArea.getSelectedText()!=null) 
			jTextArea.replaceSelection(replaceText.getText());
		}
		});//"替换"按钮监听结束
		 
		//"全部替换"按钮监听
		replaceAllButton.addActionListener(new ActionListener()
		{ public void actionPerformed(ActionEvent e)
		{ jTextArea.setCaretPosition(0); //将光标放到编辑区开头 
		int k=0,m=0,replaceCount=0;
		if(findText.getText().length()==0)
		{ JOptionPane.showMessageDialog(replaceDialog,"请填写查找内容!","提示",JOptionPane.WARNING_MESSAGE);
		 findText.requestFocus(true);
		 return;
		}
		while(k>-1)//当文本中有内容被选中时(k>-1被选中)进行替换，否则不进行while循环
		{ //"区分大小写(C)"的JCheckBox是否被选中
		 //int k=0,m=0;
		 final String str1,str2,str3,str4,strA,strB;
		 str1=jTextArea.getText();
		 str2=findText.getText();
		 str3=str1.toUpperCase();
		 str4=str2.toUpperCase();
		 if(matchCheckBox.isSelected())//区分大小写
		 { strA=str1;
		 strB=str2;
		 }
		 else//不区分大小写,此时把所选内容全部化成大写(或小写)，以便于查找 
		 { strA=str3;
		 strB=str4;
		 }
		 if(upButton.isSelected())
		 { //k=strA.lastIndexOf(strB,editArea.getCaretPosition()-1);
		 if(jTextArea.getSelectedText()==null)
		 k=strA.lastIndexOf(strB,jTextArea.getCaretPosition()-1);
		 else
		 k=strA.lastIndexOf(strB, jTextArea.getCaretPosition()-findText.getText().length()-1); 
		 if(k>-1)
		 { //String strData=strA.subString(k,strB.getText().length()+1);
			 jTextArea.setCaretPosition(k);
			 jTextArea.select(k,k+strB.length());
		 }
		 else
		 { if(replaceCount==0)
		 { JOptionPane.showMessageDialog(replaceDialog, "找不到您查找的内容!", "记事本",JOptionPane.INFORMATION_MESSAGE); 
		 }
		 else
		 { JOptionPane.showMessageDialog(replaceDialog,"成功替换"+replaceCount+"个匹配内容!","替换成功",JOptionPane.INFORMATION_MESSAGE);
		 }
		 }
		 }
		 else if(downButton.isSelected())
		 { if(jTextArea.getSelectedText()==null)
		 k=strA.indexOf(strB,jTextArea.getCaretPosition()+1);
		 else
		 k=strA.indexOf(strB, jTextArea.getCaretPosition()-findText.getText().length()+1); 
		 if(k>-1)
		 { //String strData=strA.subString(k,strB.getText().length()+1);
			 jTextArea.setCaretPosition(k);
			 jTextArea.select(k,k+strB.length());
		 }
		 else
		 { if(replaceCount==0)
		 { JOptionPane.showMessageDialog(replaceDialog, "找不到您查找的内容!", "记事本",JOptionPane.INFORMATION_MESSAGE); 
		 }
		 else
		 { JOptionPane.showMessageDialog(replaceDialog,"成功替换"+replaceCount+"个匹配内容!","替换成功",JOptionPane.INFORMATION_MESSAGE);
		 }
		 }
		 }
		 if(replaceText.getText().length()==0 && jTextArea.getSelectedText()!= null)
		 { jTextArea.replaceSelection("");
		 replaceCount++;
		 } 
		  
		 if(replaceText.getText().length()>0 && jTextArea.getSelectedText()!= null) 
		 { jTextArea.replaceSelection(replaceText.getText()); 
		 replaceCount++;
		 }
		}//while循环结束
		}
		});//"替换全部"方法结束
		 
		//创建"替换"对话框的界面
		JPanel directionPanel=new JPanel();
		directionPanel.setBorder(BorderFactory.createTitledBorder("方向"));
		//设置directionPanel组件的边框;
		//BorderFactory.createTitledBorder(String title)创建一个新标题边框，使用默认边框（浮雕化）、默认文本位置（位于顶线上）、默认调整 (leading) 以及由当前外观确定的默认字体和文本颜色，并指定了标题文本。
		directionPanel.add(upButton);
		directionPanel.add(downButton);
		JPanel panel1=new JPanel();
		JPanel panel2=new JPanel();
		JPanel panel3=new JPanel();
		JPanel panel4=new JPanel();
		panel4.setLayout(new GridLayout(2,1));
		panel1.add(findContentLabel);
		panel1.add(findText);
		panel1.add(findNextButton);
		panel4.add(replaceButton);
		panel4.add(replaceAllButton);
		panel2.add(replaceLabel);
		panel2.add(replaceText);
		panel2.add(panel4);
		panel3.add(matchCheckBox);
		panel3.add(directionPanel);
		panel3.add(cancel);
		con.add(panel1);
		con.add(panel2);
		con.add(panel3);
		replaceDialog.setSize(420,220);
		replaceDialog.setResizable(false);//不可调整大小
		replaceDialog.setLocation(230,280);
		replaceDialog.setVisible(true);
	}//"全部替换"按钮监听结束
	
    private void turnTo() {  
        final JDialog gotoDialog = new JDialog(this, "转到下列行",false); 
        JLabel gotoLabel = new JLabel("行数(L):");  
        final JTextField linenum = new JTextField(5);  
        linenum.setText("1");  
        linenum.selectAll();  
  
        JButton okButton = new JButton("确定");  
        okButton.addActionListener(new ActionListener() {  
  
            public void actionPerformed(ActionEvent e) {  
                int totalLine = jTextArea.getLineCount();  
                int[] lineNumber = new int[totalLine + 1];  
                String s = jTextArea.getText();  
                int pos = 0, t = 0;  
  
                while (true) {  
                    pos = s.indexOf('\12', pos);  
                    // System.out.println("引索pos:"+pos);  
                    if (pos == -1)  
                        break;  
                    lineNumber[t++] = pos++;  
                }  
  
                int gt = 1;  
                try {  
                    gt = Integer.parseInt(linenum.getText());  
                } catch (NumberFormatException efe) {  
                    JOptionPane.showMessageDialog(null, "请输入行数!", "提示", JOptionPane.WARNING_MESSAGE);  
                    linenum.requestFocus(true);  
                    return;  
                }  
  
                if (gt < 2 || gt >= totalLine) {  
                    if (gt < 2)  
                        jTextArea.setCaretPosition(0);  
                    else  
                        jTextArea.setCaretPosition(s.length());  
                } else  
                    jTextArea.setCaretPosition(lineNumber[gt - 2] + 1);  
  
                gotoDialog.dispose();  
            }  

        
    });  

    JButton cancelButton = new JButton("取消");  
    cancelButton.addActionListener(new ActionListener() {  
        public void actionPerformed(ActionEvent e) {  
            gotoDialog.dispose();  
        }  
    });  

    Container con = gotoDialog.getContentPane();  
    con.setLayout(new FlowLayout());  
    con.add(gotoLabel);  
    con.add(linenum);  
    con.add(okButton);  
    con.add(cancelButton);  

    gotoDialog.setSize(200, 100);  
    gotoDialog.setResizable(false);  
    gotoDialog.setLocation(300, 280);  
    gotoDialog.setVisible(true);  
    }
	
	/*
	 * 组件添加事件，，
	 */	
	public void Event() {
		
		//以下为文件菜单
		newItem.addActionListener(new ActionListener() {
			   public void actionPerformed(ActionEvent e) {
				    try {
				     if (e.getSource() == newItem) {
				      if (!(getTa().getText()).equals("")) {
				       Object[] options = { "确定", "取消" };
				       int response = JOptionPane.showOptionDialog(null,
				         "你是否保存", "提示", JOptionPane.YES_OPTION,
				         JOptionPane.QUESTION_MESSAGE, null,
				         options, options[0]);
				       if (response == 0) {
				        FileDialog d = new FileDialog(f, "保存文件",
				          FileDialog.SAVE);
				        d.setVisible(true);
				        fileName = d.getDirectory() + d.getFile();
				        FileOutputStream fout = new FileOutputStream(
				          fileName + ".txt");

				        byte[] bb = getTa().getText()
				          .getBytes();

				        fout.write(bb);
				        // 关闭
				        fout.close();
				        JOptionPane.showMessageDialog(null, "已保存");
				        getTa().setText("");
				       }
				       if (response == 1) {
				        JOptionPane.showMessageDialog(null, "你选择了取消");
				        getTa().setText("");
				       }
				      }
				     }
				    } catch (Exception e2) {
				     System.out.println(e2.getMessage());
				    }
				   }
				  });
		
		closeItem.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				System.exit(0);
			}
		});
		
		aboutItem.addActionListener(new ActionListener() {		
			@Override
			public void actionPerformed(ActionEvent e) {
				JOptionPane.showMessageDialog(null, "windows记事本\n"
						+ "借鉴@SnoWalker\n" + "用于实现");
			}
		});
		
		 openItem.addActionListener(new ActionListener()//菜单条目监听：打开  
	        {  
	            public void actionPerformed(ActionEvent e)  
	            {  
	                open.setVisible(true);  
	                String dirPath = open.getDirectory();	//获取对话框目录；FileDialog类的方法  
	                String fileName= open.getFile();    	//获取对话框选定文件  
	                if(dirPath==null || fileName==null) 	//点取消  
	                    return; 
	                
	                jTextArea.setText("");//打开文件之前清空文本区域  
	                
	                file = new File(dirPath,fileName);  
	                try  
	                {  
	                    BufferedReader br = new BufferedReader(new FileReader(file));//放入缓存器提高效率  
	                    String line = null;		//定义一个空行
	                    while ((line=br.readLine()) !=null)  
	                    {  
	                    	//将给定文本追加到文档结尾。如果模型为 null 或者字符串为 null 或空，则不执行任何操作。 
	                    	//虽然大多数 Swing 方法不是线程安全的，但此方法是线程安全的。
	                    	jTextArea.append(line+"\r\n");  
	                    }  
	                }  
	                catch (IOException ie){  
	                    throw new RuntimeException("读取失败！");  
	                }  
	            }  
	        });  
		 
	        saveItem.addActionListener(new ActionListener()//菜单条目监听：保存  
	        {     
	            public void actionPerformed(ActionEvent e)  
	            {  
	                if(file==null)  
	                {  
	                    save.setVisible(true);  
	                    String dirPath = save.getDirectory();  
	                    String fileName= save.getFile();  
	                    if(dirPath==null || fileName==null)  
	                        return;  
	                    file = new File(dirPath,fileName);                
	                }  
	                try  
	                {  
	                    BufferedWriter bw = new BufferedWriter(new FileWriter(file));  
	                    String text = jTextArea.getText();  
	                    bw.write(text);  
	                    bw.close();  
	                }  
	                catch (IOException ex)  
	                {  
	                    throw new RuntimeException();  
	                }  
	            }  
	        }); 
	        
	        savetoItem.addActionListener(new ActionListener() {
	     	   public void actionPerformed(ActionEvent e) {
	     		    if (e.getSource() == savetoItem) {
	     		     try {
	     		      FileDialog d = new FileDialog(f, "另存为", FileDialog.SAVE);
	     		      d.setVisible(true);
	     		      fileName = d.getDirectory() + d.getFile();
	     		      FileOutputStream fout = new FileOutputStream(fileName + ".txt");
	     		      byte[] bb = getTa().getText().getBytes();

	     		      fout.write(bb);
	     		      // 关闭
	     		      fout.close();
	     		     } catch (Exception e4) {
	     		      System.out.println(e4.getMessage());
	     		     }
	     		    }
	     		   }
	     		  });
	        
	        
	 
	        
	        //以下为编辑菜单
	        editUndo.addActionListener(new ActionListener() {
		     	   public void actionPerformed(ActionEvent e) {
		     		  jTextArea.requestFocus();
		     		 if(undo.canUndo())
		     		 { try
		     		 { undo.undo();
		     		 }
		     		 catch (CannotUndoException ex)
		     		 { System.out.println("Unable to undo:" + ex);
		     		  //ex.printStackTrace();
		     		 }
		     		 }
		     		 if(!undo.canUndo())
		     		 { editUndo.setEnabled(false);
		     		 }
		     		   }
		     		  });
	        editCut.addActionListener(new ActionListener() {
	     	   public void actionPerformed(ActionEvent e) {
	     	    if (e.getSource() == editCut) {
	     	    	jTextArea.requestFocus();
	     	    	String text=jTextArea.getSelectedText();
	     	    	StringSelection selection=new StringSelection(text);
	     	    	clipBoard.setContents(selection,null);
	     	    	jTextArea.replaceRange("",jTextArea.getSelectionStart(),jTextArea.getSelectionEnd());
	     	    	checkMenuItemEnabled();
	     	    	
	     	    }
	     	   }
	     	  });
	        editCopy.addActionListener(new ActionListener() {
	     	   public void actionPerformed(ActionEvent e) {
	     	    if (e.getSource() == editCopy) {
	     	    	jTextArea.requestFocus();
	     	    	String text=jTextArea.getSelectedText();
	     	    	StringSelection selection=new StringSelection(text);
	     	    	clipBoard.setContents(selection,null);
	     	    	checkMenuItemEnabled();
	     	    }
	     	   }
	     	  });
	  	  editPaste.addActionListener(new ActionListener() {
	  	   public void actionPerformed(ActionEvent e) {
	  	    if (e.getSource() == editPaste) {
	  	    	jTextArea.requestFocus();
	  	    	Transferable contents=clipBoard.getContents(this);
	  	    	if(contents==null)return;
	  	    	String text="";
	  	    	try
	  	    	{ text=(String)contents.getTransferData(DataFlavor.stringFlavor);
	  	    	}
	  	    	catch (Exception exception)
	  	    	{
	  	    	}
	  	    	jTextArea.replaceRange(text,jTextArea.getSelectionStart(),jTextArea.getSelectionEnd());
	  	    	checkMenuItemEnabled();
	  	    }
	  	   }
	  	  });
	  	  editDelete.addActionListener(new ActionListener() {
		  	   public void actionPerformed(ActionEvent e) {
			  	    if (e.getSource() == editDelete) {
			  	    	jTextArea.requestFocus();
			  	    	jTextArea.replaceRange("",jTextArea.getSelectionStart(),jTextArea.getSelectionEnd());
			  	    	checkMenuItemEnabled();
			  	   }
		  	   }
			  	  });
	  	 editFind.addActionListener(new ActionListener() {
		  	   public void actionPerformed(ActionEvent e) {
			  	    if (e.getSource() == editFind) {
			  	    	jTextArea.requestFocus();
			  	    	find();
			  	   }
		  	   }
			  	  });
	  	editReplace.addActionListener(new ActionListener() {
		  	   public void actionPerformed(ActionEvent e) {
			  	    if (e.getSource() == editReplace) {
			  	    	jTextArea.requestFocus();
			  	    	replace();
			  	   }
		  	   }
			  	  });
	  	
	  	editGoto.addActionListener(new ActionListener() {
	  	   public void actionPerformed(ActionEvent e) {
		  	    if (e.getSource() == editGoto) {
		  	    	jTextArea.requestFocus();
		  	    	turnTo();
		  	   }
	  	   }
		  	  });
	  	
	  	editAll.addActionListener(new ActionListener() {
	  	   public void actionPerformed(ActionEvent e) {
		  	    if (e.getSource() == editAll) {
		  	    	jTextArea.selectAll();
		  	   }
	  	   }
		  	  });
	  	
	  	formatLinewrap.addActionListener(new ActionListener() {
		  	   public void actionPerformed(ActionEvent e) {
		  		 if(formatLinewrap.getState())
		  			jTextArea.setLineWrap(true);
		  			else
		  			jTextArea.setLineWrap(false);
		  	   }
			  	  });
	  	formatFont.addActionListener(new ActionListener() {
		  	   public void actionPerformed(ActionEvent e) {
		  		 jTextArea.requestFocus();
		  		font();
		  	   }
			  	  });
	  	Status.addActionListener(new ActionListener() {
		  	   public void actionPerformed(ActionEvent e) {
		  		 if(Status.getState()) {
		  		 statusLabel.setVisible(true);
		  		 }
		  		else
		  		statusLabel.setVisible(false);
		  	   }
			  	  });
	}
		
	public static void main(String[] args){
		new MainFrame();
	}
}
