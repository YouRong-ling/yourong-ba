# 单例模式
<?php
class Db{
	static private $_instance;
	static private $_connectSource;
	private $_dbConfig = [
		'host' => '127.0.0.1',
		'user' => 'root',
		'password' => '123456',
		'database' => 'hanling'
	];
	
	private function __construct(){
		
	}
	
	static public function getInstance(){
		if(!(self::$_instance instanceof self)){
			self::$_instance = new self();
		}
		return self::$_instance;
	}
	
	public function connect(){
		if(!self::$_connectSource){
			self::$_connectSource = mysql_connect($this->_dbConfig['host'],$this->_dbConfig['user'],$this->_dbConfig['password']);
			if(!self::$_connectSource){
				die('mysql connect error'.mysql_error());
			}
			mysql_select_db($this->_dbConfig['database'],self::$_connectSource);
			mysql_query('set names utf8',self::$_connectSource);
		}
		return self::$_connectSource;
	}
}

$connect = Db::getInstance()->connect();
var_dump($connect);//资源1

?>
