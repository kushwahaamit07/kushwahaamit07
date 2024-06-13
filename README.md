pragma solidity ^0.8.0;

contract MyToken {
    // Public variables
    string public tokenName = "META";
    string public tokenSymbol = "MTA";
    uint public totalSupply = 0;

    // Mapping variable
    mapping(address => uint) public balances;

    // Event emitted when tokens are minted or burned
    event Transfer(address indexed from, address indexed to, uint value);

    // Modifier to check if the caller is the owner
    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can call this function");
        _;
    }

    // Owner of the contract
    address public owner;

    // Constructor to set the owner
    constructor() {
        owner = msg.sender;
    }

    // Mint function
    function mint(address _address, uint _value) public onlyOwner {
        totalSupply += _value;
        balances[_address] += _value;
        emit Transfer(address(0), _address, _value);
    }

    // Burn function
    function burn(address _address, uint _value) public onlyOwner {
        if (balances[_address] >= _value) {
            totalSupply -= _value;
            balances[_address] -= _value;
            emit Transfer(_address, address(0), _value);
        }
    }
}
